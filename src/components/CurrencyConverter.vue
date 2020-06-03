<template>
  <div class="flex flex-col justify-center bg-indigo-600">
    <div class="flex">
      <div class="w-3/6 justify-center mx-2">
        <input type="text" class="text-xs rounded overflow-hidden" v-model="currencyFrom" @click="isHidden = !isHidden">
            <button v-if="isHidden" @click="isHidden = false" tabindex="-1" class="fixed inset-0 h-full w-full cursor-default"></button>
        <div v-show='isHidden' class="absolute rounded-lg shadow-xl bg-white overflow-hidden" :class="{'h-20': heightOverflow}" style="overflow-y:auto">
          <a href="#" class="block text-xs py-1 px-2 hover:bg-gray-100" v-for="currency in filteredList" :key="currency" @click="currencyFrom = currency; isHidden = !isHidden">{{currency}}</a>
        </div>
      </div>

      <div class="w-2/6 mr-2">
        <input type="text" class="text-xs rounded w-full" :placeholder="someText">
      </div>
    </div>
    <div class="flex">
      <div class="">Again</div>
      <div class="">Hi</div>
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
      currencies: ['Afghan Afghani', 'Albanian Lek', 'Algerian Dinar', 'Angolan Kwanza', 'Argentine Peso', 'Armenian Dram', 'Aruban Florin', 'Australian Dollar', 'Azerbaijani Manat', 'Bahamian Dollar', 'Bahraini Dinar', 'Bajan dollar', 'Bangladeshi Taka', 'Belarusian Ruble', 'Belize Dollar', 'Bermudan Dollar', 'Bhutan currency', 'Bitcoin', 'Bitcoin Cash', 'Bolivian Boliviano', 'Bosnia-Herzegovina Convertible Mark', 'Botswanan Pula', 'Brazilian Real', 'Brunei Dollar', 'Bulgarian Lev', 'Burundian Franc', 'CFP Franc', 'Cambodian riel', 'Canadian Dollar', 'Cape Verdean Escudo', 'Cayman Islands Dollar', 'Central African CFA franc', 'Chilean Peso', 'Chilean Unit of Account (UF)', 'Chinese Yuan', 'Chinese Yuan (offshore)', 'Colombian Peso', 'Comorian franc', 'Congolese Franc', 'Costa Rican Colón', 'Croatian Kuna', 'Cuban Peso', 'Czech Koruna', 'Danish Krone', 'Djiboutian Franc', 'Dominican Peso', 'East Caribbean Dollar', 'Egyptian Pound', 'Ether', 'Ethiopian Birr', 'Euro', 'Fijian Dollar', 'Gambian dalasi', 'Georgian Lari', 'Ghanaian Cedi', 'Guatemalan Quetzal', 'Guinean Franc', 'Guyanaese Dollar', 'Haitian Gourde', 'Honduran Lempira', 'Hong Kong Dollar', 'Hungarian Forint', 'Icelandic Króna', 'Indian Rupee', 'Indonesian Rupiah', 'Iranian Rial', 'Iraqi Dinar', 'Israeli New Shekel', 'Jamaican Dollar', 'Japanese Yen', 'Jordanian Dinar', 'Kazakhstani Tenge', 'Kenyan Shilling', 'Kuwaiti Dinar', 'Kyrgystani Som', 'Laotian Kip', 'Lebanese pound', 'Lesotho loti', 'Liberian Dollar', 'Libyan Dinar', 'Litecoin', 'Macanese Pataca', 'Macedonian Denar', 'Malagasy Ariary', 'Malawian Kwacha', 'Malaysian Ringgit', 'Maldivian Rufiyaa', 'Mauritanian Ouguiya', 'Mauritian Rupee', 'Mexican Peso', 'Moldovan Leu', 'Moroccan Dirham', 'Mozambican metical', 'Myanmar Kyat', 'NT$', 'Namibian dollar', 'Nepalese Rupee', 'Netherlands Antillean Guilder', 'New Zealand Dollar', 'Nicaraguan Córdoba', 'Nigerian Naira', 'Norwegian Krone', 'Omani Rial', 'Pakistani Rupee', 'Panamanian Balboa', 'Papua New Guinean Kina', 'Paraguayan Guarani', 'Philippine peso', 'Poland złoty', 'Pound sterling', 'Qatari Rial', 'Romanian Leu', 'Russian Ruble', 'Rwandan franc', 'Salvadoran Colón', 'Saudi Riyal', 'Serbian Dinar', 'Seychellois Rupee', 'Sierra Leonean Leone', 'Singapore Dollar', 'Sol', 'Solomon Islands Dollar', 'Somali Shilling', 'South African Rand', 'South Korean won', 'Sovereign Bolivar', 'Sri Lankan Rupee', 'Sudanese pound', 'Surinamese Dollar', 'Swazi Lilangeni', 'Swedish Krona', 'Swiss Franc', 'Tajikistani Somoni', 'Tanzanian Shilling', 'Thai Baht', "Tongan Pa'anga", 'Trinidad and Tobago Dollar', 'Tunisian Dinar', 'Turkish lira', 'Turkmenistan manat', 'Ugandan Shilling', 'Ukrainian hryvnia', 'United Arab Emirates Dirham', 'United States Dollar', 'Uruguayan Peso', 'Uzbekistani Som', 'Vietnamese dong', 'West African CFA franc', 'Yemeni Rial', 'Zambian Kwacha'],
      currencyFrom: '',
      isHidden: false,
      heightOverflow: true,
      currencyTo: '',
      someText: '0.0'
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
    handler: function (event) {
      (async () => {
        try {
          const html = await got(`https://www.google.com/search?q=${this.currencyFrom}+to+${this.currencyTo}`)
          const $ = cheerio.load(html.body)
          let value = $('.iBp4i')
          value = value.text().split(' ')[0]
          this.someText = value
        } catch (error) {
          console.log(error.response.body)
        }
      })()
    }
  },
  computed: {
    filteredList () {
      const filteredValue = this.currencies.filter(currency => {
        return currency.toLowerCase().includes(this.currencyFrom.toLowerCase())
      })
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      this.heightOverflow = (filteredValue.length > 3)
      return filteredValue
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
