<template>
  <div class="flex items-center flex-col justify-center w-56 h-full">
    <div class="flex flex-col bg-red-200 font-mono w-full h-full rounded-t" >

      <div class="flex justify-end" style="-webkit-app-region: drag;">
        <img class="h-4 w-4 m-1" src="./../assets/images/icon.svg" />
        <p class="text-xs text-red-600 leading-snug mt-1 mr-12"> Currency Converter</p>
        <button class="no-outline" id="btn-minimize" style="-webkit-app-region: no-drag;" @click="minimize()">
<!-- Generator: Adobe Illustrator 19.0.0, SVG Export Plug-In . SVG Version: 6.00 Build 0)  -->
<svg class="w-2 h-2 fill-current text-blue-900 mr-1" version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
  viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve">
<g>
<g>
  <path d="M492,236H20c-11.046,0-20,8.954-20,20c0,11.046,8.954,20,20,20h472c11.046,0,20-8.954,20-20S503.046,236,492,236z"/>
</g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
</svg>
        </button>
        <button class="rounded-tr-lg no-outline" id="btn-close" style="-webkit-app-region: no-drag;" @click='closeWindow()'>
          <svg class="h-5 w-5 fill-current text-red-200" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg"><path d="m416 512h-320c-53.023438 0-96-42.976562-96-96v-320c0-53.023438 42.976562-96 96-96h320c53.023438 0 96 42.976562 96 96v320c0 53.023438-42.976562 96-96 96zm0 0" /><g fill="#fc573b"><path d="m342.734375 312.574219-143.308594-143.308594c-6.257812-6.257813-16.386719-6.257813-22.625 0l-7.535156 7.535156c-6.257813 6.253907-6.257813 16.382813 0 22.625l143.308594 143.308594c6.257812 6.257813 16.386719 6.257813 22.625 0l7.535156-7.535156c6.257813-6.253907 6.257813-16.382813 0-22.625zm0 0"/><path d="m312.574219 169.265625-143.308594 143.308594c-6.257813 6.257812-6.257813 16.386719 0 22.625l7.535156 7.535156c6.253907 6.257813 16.382813 6.257813 22.625 0l143.308594-143.308594c6.257813-6.257812 6.257813-16.386719 0-22.625l-7.535156-7.535156c-6.253907-6.257813-16.382813-6.257813-22.625 0zm0 0"/></g></svg>
        </button>
      </div>
    </div>
    <div class="flex flex-col w-56 rounded font-mono">
  <div class="flex flex-col h-48 flex-row bg-red-500 justify-center items-center">
    <div class="w-3/6">
      <input class="text-3xl block bg-red-500 text-white outline-none rounded-lg block w-full appearance-none leading-normal text-center placeholder-gray-100"
      v-model="currencyFrom.value" @keyup="handler()" @focus="currencyFrom.value = '' ;handler()" type="text" :placeholder="currencyFrom.value">
      <hr>
    </div>
    <div class="w-3/6 pt-5">
      <input class="block bg-red-500 text-white outline-none rounded-lg block w-full appearance-none tracking-tighter leading-normal text-center placeholder-gray-100"
      v-model="currencyFrom.name" @focus="currencyFrom.name = '' ;handler()" @click="currencyFrom.isHidden = !currencyFrom.isHidden; handler()"
      type="text" :placeholder="currencyFrom.name">
      <button v-if="currencyFrom.isHidden" @click="currencyFrom.isHidden = false" tabindex="-1" class="fixed inset-0 h-full w-full cursor-default"></button>
      <div v-show='currencyFrom.isHidden' class="mt-1 absolute rounded w-32 shadow-xl bg-white overflow-hidden" :class="{'h-10': currencyFrom.heightOverflow}" style="overflow-y:auto">
        <a href="#" class="block text-xs py-1 px-2 hover:bg-gray-100" v-for="currency in filteredListFrom" :key="currency" @click="currencyFrom.name = currency; currencyFrom.isHidden = !currencyFrom.isHidden; handler()">{{currency}}</a>
      </div>
      <hr>
    </div>
    <div class="self-start mt-24 pl-3 absolute">
      <button @click="switchhandler()" class="block rounded bg-red-100 shadow-xl focus:outline-none hover:bg-red-300">
        <svg class="p-1 w-8 h-8 fill-current hover:text-gray-100 text-red-400" id="Layer" enable-background="new 0 0 64 64" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg"><path d="m31.414 15.586-7-7c-.78-.781-2.048-.781-2.828 0l-7 7c-.781.781-.781 2.047 0 2.828.78.781 2.048.781 2.828 0l3.586-3.586v39.172c0 1.104.896 2 2 2s2-.896 2-2v-39.172l3.586 3.586c.39.391.902.586 1.414.586s1.024-.195 1.414-.586c.781-.781.781-2.047 0-2.828z"/><path d="m46.586 45.586-3.586 3.586v-39.172c0-1.104-.896-2-2-2s-2 .896-2 2v39.172l-3.586-3.586c-.78-.781-2.048-.781-2.828 0-.781.781-.781 2.047 0 2.828l7 7c.39.391.902.586 1.414.586s1.024-.195 1.414-.586l7-7c.781-.781.781-2.047 0-2.828-.78-.781-2.048-.781-2.828 0z"/></svg>
      </button>
    </div>
  </div>
  <div class="flex flex-col h-48 rounded-b flex-row bg-gray-100 justify-center items-center" style="caret-color:rgba(252,129,129,1)">
    <div class="w-3/6">
      <p class="text-3xl block bg-gray-100 text-red-400 outline-none rounded-lg block w-full appearance-none tracking-tighter leading-normal text-center"
      type="text">{{currencyTo.value}}</p>
      <hr>
    </div>
    <div class="w-3/6 pt-5">
      <input class="tracking-tighter block bg-gray-100 text-red-400 outline-none rounded-lg block w-full appearance-none leading-normal text-center placeholder-red-400"
      v-model="currencyTo.name" @click="currencyTo.isHidden = !currencyTo.isHidden" @focus="currencyTo.name = '' ;handler()"
      type="text" :placeholder="currencyTo.name">
      <button v-if="currencyTo.isHidden" @click="currencyTo.isHidden = false" tabindex="-1" class="fixed inset-0 h-full w-full cursor-default"></button>
      <div v-show='currencyTo.isHidden' class=" mt-1 w-32 absolute rounded shadow-xl bg-white overflow-hidden" :class="{'h-10': currencyTo.heightOverflow}" style="overflow-y:auto">
        <a href="#" class="block text-xs py-1 px-2 hover:bg-red-300" v-for="currency in filteredListTo" :key="currency" @click="currencyTo.name = currency; currencyTo.isHidden = !currencyTo.isHidden; handler()">{{currency}}</a>
      </div>
      <hr>
    </div>
  </div>
</div>
  </div>
</template>

<script>
const { BrowserWindow } = require('electron').remote
const got = require('got')
const cheerio = require('cheerio')

export default {
  name: 'CurrencyConverter',
  data () {
    return {
      currencies: ['Afghan Afghani - AFN', 'Albanian Lek - ALL', 'Algerian Dinar - DZD', 'Angolan Kwanza - AOA', 'Argenti ne Peso - ARS', 'Armenian Dram - AMD', 'Aruban Florin - AWG', 'Australian Dollar - AUD', 'Azerbaijani M anat - AZN', 'Bahamian Dollar - BSD', 'Bahraini Dinar - BHD', 'Bajan Dollar - BBD', 'Bangladeshi Taka - BDT', 'Belarusian Ruble - BYR', 'Belize Dollar - BZD', 'Bermudan Dollar - BMD', 'Bhutan currency - BTN ', 'Bitcoin Cash - XBT', 'Bolivian Boliviano - BOB', 'Bosnia-Herzegovina Convertible Mark - BAM', 'Bots wanan Pula - BWP', 'Brazilian Real - BRL', 'Brunei Dollar - BND', 'Bulgarian Lev - BGN', 'Burundian Fra nc - BIF', 'CFP Franc - XPF', 'Cambodian riel - KHR', 'Canadian Dollar - CAD', 'Cape Verdean Escudo - C VE', 'Cayman Islands Dollar - KYD', 'Central African CFA Franc - FCFA', 'Chilean Peso - CLP', 'Chilean Unit of Account (UF) - CLF', 'Chinese Yuan - CNY', 'Chinese Yuan (offshore) - CNY', 'Colombian Peso - C OP', 'Comorian Franc - CF', 'Congolese Franc - CDF', 'Costa Rican Colón - CRC', 'Croatian Kuna - HRK', 'Cuban Peso - CUC', 'Czech Koruna - CZK', 'Danish Krone - DKK', 'Djiboutian Franc - DJF', 'Dominican Pe so - DOP', 'East Caribbean Dollar - XCD', 'Egyptian Pound - EGP', 'Ethiopian Birr - ETB', 'Fijian Dolla r - FJD', 'Gambian dalasi - GMD', 'Georgian Lari - GEL', 'Ghanaian Cedi - GHS', 'Guatemalan Quetzal - G TQ', 'Guinean Franc - GNF', 'Guyanaese Dollar - GYD', 'Haitian Gourde - HTG', 'Honduran Lempira - HNL', 'Hong Kong Dollar - HKD', 'Hungarian Forint - HUF', 'Icelandic Króna - ISK', 'Indian Rupee - INR', 'In donesian Rupiah - IDR', 'Iranian Rial - IRR', 'Iraqi Dinar - IQD', 'Israeli New Shekel - ILS', 'Jamaica n Dollar - JMD', 'Japanese Yen - JPY', 'Jordanian Dinar - JOD', 'Kazakhstani Tenge - KZT', 'Kenyan Shil ling - KES', 'Kuwaiti Dinar - KWD', 'Kyrgystani Som - KGS', 'Laotian Kip - LAK', 'Lebanese pound - LBP', 'Lesotho Loti - LSL', 'Liberian Dollar - LRD', 'Libyan Dinar - LYD', 'Macanese Pataca - MOP', 'Macedo nian Denar - MKD', 'Malagasy Ariary - MGA', 'Malawian Kwacha - MWK', 'Malaysian Ringgit - MYR', 'Maldiv ian Rufiyaa - MVR', 'Mauritanian Ouguiya - MRO', 'Mauritian Rupee - MUR', 'Mexican Peso - MXN', 'Moldov an Leu - MDL', 'Moroccan Dirham - MAD', 'Mozambican metical - MZN', 'Myanmar Kyat - MMK', 'Namibian dol lar - NAD', 'Nepalese Rupee - NPR', 'Netherlands Antillean Guilder - ANG', 'New Zealand Dollar - NZD', 'Nicaraguan Córdoba - NIO', 'Nigerian Naira - NGN', 'Norwegian Krone - NOK', 'Omani Rial - OMR', 'Pakis tani Rupee - PKR', 'Panamanian Balboa - PAB', 'Papua New Guinean Kina - PGK', 'Paraguayan Guarani - PYG ', 'Philippine peso - PHP', 'Poland Złoty - PLN', 'Pound sterling - EGP', 'Qatari Rial - QAR', 'Romania n Leu - RON', 'Russian Ruble - RUB', 'Rwandan franc - RWF', 'Salvadoran Colón - SVC', 'Saudi Riyal - SA R', 'Serbian Dinar - RSD', 'Seychellois Rupee - SCR', 'Sierra Leonean Leone - SLL', 'Singapore Dollar - SGD', 'Solomon Islands Dollar - SBD', 'Somali Shilling - SOS', 'South African Rand - ZAR', 'South Kore an won - KRW', 'Sovereign Bolivar - VES', 'Sri Lankan Rupee - LKR', 'Sudanese pound - SDG', 'Surinamese Dollar - SRD', 'Swazi Lilangeni - SZL', 'Swedish Krona - SEK', 'Swiss Franc - CHF', 'Tajikistani Somon i - TJS', 'Tanzanian Shilling - TZS', 'Thai Baht - THB', "Tongan Pa'anga - TOP", 'Trinidad and Tobago D ollar - TTD', 'Tunisian Dinar - TND', 'Turkish lira - TRY', 'Turkmenistan manat - TMT', 'Ugandan Shilli ng - UGX', 'Ukrainian hryvnia - UAH', 'United Arab Emirates Dirham - AED', 'United States Dollar - USD', 'Uruguayan Peso - UYU', 'Uzbekistani Som - UZS', 'Vietnamese dong - VND', 'West African CFA franc - X OF', 'Yemeni Rial - YER', 'Zambian Kwacha - ZMW', 'Bitcoin - XBT', 'Ether - ETH', 'Euro - EUR', 'Liteco in - LTC', 'NT$ - TWD', 'Peruvian Sol - PEN'],
      currencyFrom: {
        name: 'Currency From',
        value: '0.0',
        isHidden: false,
        heightOverflow: true
      },
      currencyTo: {
        name: 'Currency To',
        value: '0.0',
        isHidden: false,
        heightOverflow: true
      }
    }
  },
  mounted () {
    window.addEventListener('keydown', this.handler)
  },
  beforeDestroy () {
    window.removeEventListener('keydown', this.handler)
  },
  methods: {
    evaluate: function evaluate () {
      let handledResult = 0
      try {
        // eslint-disable-next-line no-eval
        handledResult = eval(this.x)
      } catch (SyntaxError) {
        console.log(SyntaxError.message)
        return
      }
      if (Number.isInteger(handledResult)) {
        this.result = handledResult
      } else {
        this.result = parseFloat(handledResult.toString().split('.')[0] + '.' + handledResult.toString().split('.')[1].slice(0, 5))
      }
    },
    minimize: function () {
      BrowserWindow.getFocusedWindow().minimize()
    },
    closeWindow: function () {
      BrowserWindow.getFocusedWindow().close()
    },
    handler: function () {
      if (this.currencies.includes(this.currencyFrom.name) && this.currencies.includes(this.currencyTo.name)) {
        if (parseInt(this.currencyFrom.value) === 0) {
          this.currencyTo.value = '0.00'
        } else if (this.currencyFrom.name === this.currencyTo.name) {
          this.currencyTo.value = this.currencyFrom.value
        } else {
          (async () => {
            try {
              const html = await got(`https://www.google.com/search?q=${this.currencyFrom.name}+to+${this.currencyTo.name}`)
              const $ = cheerio.load(html.body)
              let value = $('.iBp4i')
              value = value.text().split(' ')[0]
              this.currencyTo.value = (isNaN(parseFloat(this.currencyFrom.value)) ? 0 : parseFloat(this.currencyFrom.value) * value).toFixed(2)
            } catch (error) {
              console.log(error.response.body)
            }
          })()
        }
      }
    },
    switchhandler: function () {
      const temp = this.currencyFrom
      this.currencyFrom = this.currencyTo
      this.currencyTo = temp
    }
  },
  computed: {
    filteredListFrom () {
      const filteredValue = this.currencies.filter(currency => {
        return currency.toLowerCase().includes(this.currencyFrom.name.toLowerCase())
      })
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.currencyFrom.heightOverflow = (filteredValue.length > 3)
      return filteredValue
    },
    filteredListTo () {
      const filteredValue = this.currencies.filter(currency => {
        return currency.toLowerCase().includes(this.currencyTo.name.toLowerCase())
      })
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.currencyTo.heightOverflow = (filteredValue.length > 3)
      return filteredValue
    },
    // eslint-disable-next-line vue/return-in-computed-property
    convertCurrency () {
      if (this.currencies.includes(this.currencyFrom.name) && this.currencies.includes(this.currencyTo.name)) {
        this.handler()
      }
    }
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>
/* ::-webkit-scrollbar {
    width: 0.5em !important;
    scroll-behavior: smooth !important;
}

::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3) !important;
}

::-webkit-scrollbar-thumb {
    background-color: darkgrey !important;
    outline: 1px solid slategrey !important;
    border-radius: 10px;
} */
::-webkit-scrollbar-thumb {
  background-color: rgb(134, 131, 131);
  border: 4px solid transparent;
  border-radius: 10px;
  /* background-clip: padding-box; */
  height: 16px;
  border: 1px solid rgb(194, 190, 190);
}

::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(145, 139, 139, 0.3);
  background-color: #F5F5F5;
  border-radius: 10px;

}
::-webkit-scrollbar {
  width: 10px;
}
  .no-outline {
    outline: 0!important;
  }
</style>
