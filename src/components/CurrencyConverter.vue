<template>
  <div class="flex flex-col justify-center bg-purple-600">
    <div class="my-2">
      <form action="/action_page.php">
        <select v-model="currencyFrom" class="w-3/6 ml-2 text-xs py-1 px-1 rounded appearance-none bg-white border border-gray-400 hover:border-gray-500 rounded shadow leading-tight focus:outline-none focus:shadow-outline">
          <option value="" selected>select</option>
          <option v-for="currency in currencies" :key="currency">{{currency}}</option>
        </select>
        <input class="appearance-none w-2/6 ml-2 bg-gray-200 text-xs text-gray-700 border border-gray-400 rounded py-1 px-1 leading-tight focus:outline-none focus:bg-white" id="grid-first-name" type="text" placeholder="0.00">
        <label>{{currencyFrom}}</label>
      </form>
    </div>
    <p>{{someText}}</p>
    <button @click="handler()">submit</button>
  </div>
</template>

<script>
const { BrowserWindow } = require('electron').remote
// const Nightmare = require('nightmare')
// const nightmare = Nightmare({ show: true })
// const puppeteer = require('puppeteer')

export default {
  name: 'CurrencyConverter',
  data () {
    return {
      currencies: ['Afghan Afghani', 'Albanian Lek', 'Algerian Dinar', 'Angolan Kwanza', 'Argentine Peso', 'Armenian Dram', 'Aruban Florin', 'Australian Dollar', 'Azerbaijani Manat', 'Bahamian Dollar', 'Bahraini Dinar', 'Bajan dollar', 'Bangladeshi Taka', 'Belarusian Ruble', 'Belize Dollar', 'Bermudan Dollar', 'Bhutan currency', 'Bitcoin', 'Bitcoin Cash', 'Bolivian Boliviano', 'Bosnia-Herzegovina Convertible Mark', 'Botswanan Pula', 'Brazilian Real', 'Brunei Dollar', 'Bulgarian Lev', 'Burundian Franc', 'CFP Franc', 'Cambodian riel', 'Canadian Dollar', 'Cape Verdean Escudo', 'Cayman Islands Dollar', 'Central African CFA franc', 'Chilean Peso', 'Chilean Unit of Account (UF)', 'Chinese Yuan', 'Chinese Yuan (offshore)', 'Colombian Peso', 'Comorian franc', 'Congolese Franc', 'Costa Rican Colón', 'Croatian Kuna', 'Cuban Peso', 'Czech Koruna', 'Danish Krone', 'Djiboutian Franc', 'Dominican Peso', 'East Caribbean Dollar', 'Egyptian Pound', 'Ether', 'Ethiopian Birr', 'Euro', 'Fijian Dollar', 'Gambian dalasi', 'Georgian Lari', 'Ghanaian Cedi', 'Guatemalan Quetzal', 'Guinean Franc', 'Guyanaese Dollar', 'Haitian Gourde', 'Honduran Lempira', 'Hong Kong Dollar', 'Hungarian Forint', 'Icelandic Króna', 'Indian Rupee', 'Indonesian Rupiah', 'Iranian Rial', 'Iraqi Dinar', 'Israeli New Shekel', 'Jamaican Dollar', 'Japanese Yen', 'Jordanian Dinar', 'Kazakhstani Tenge', 'Kenyan Shilling', 'Kuwaiti Dinar', 'Kyrgystani Som', 'Laotian Kip', 'Lebanese pound', 'Lesotho loti', 'Liberian Dollar', 'Libyan Dinar', 'Litecoin', 'Macanese Pataca', 'Macedonian Denar', 'Malagasy Ariary', 'Malawian Kwacha', 'Malaysian Ringgit', 'Maldivian Rufiyaa', 'Mauritanian Ouguiya', 'Mauritian Rupee', 'Mexican Peso', 'Moldovan Leu', 'Moroccan Dirham', 'Mozambican metical', 'Myanmar Kyat', 'NT$', 'Namibian dollar', 'Nepalese Rupee', 'Netherlands Antillean Guilder', 'New Zealand Dollar', 'Nicaraguan Córdoba', 'Nigerian Naira', 'Norwegian Krone', 'Omani Rial', 'Pakistani Rupee', 'Panamanian Balboa', 'Papua New Guinean Kina', 'Paraguayan Guarani', 'Philippine peso', 'Poland złoty', 'Pound sterling', 'Qatari Rial', 'Romanian Leu', 'Russian Ruble', 'Rwandan franc', 'Salvadoran Colón', 'Saudi Riyal', 'Serbian Dinar', 'Seychellois Rupee', 'Sierra Leonean Leone', 'Singapore Dollar', 'Sol', 'Solomon Islands Dollar', 'Somali Shilling', 'South African Rand', 'South Korean won', 'Sovereign Bolivar', 'Sri Lankan Rupee', 'Sudanese pound', 'Surinamese Dollar', 'Swazi Lilangeni', 'Swedish Krona', 'Swiss Franc', 'Tajikistani Somoni', 'Tanzanian Shilling', 'Thai Baht', "Tongan Pa'anga", 'Trinidad and Tobago Dollar', 'Tunisian Dinar', 'Turkish lira', 'Turkmenistan manat', 'Ugandan Shilling', 'Ukrainian hryvnia', 'United Arab Emirates Dirham', 'United States Dollar', 'Uruguayan Peso', 'Uzbekistani Som', 'Vietnamese dong', 'West African CFA franc', 'Yemeni Rial', 'Zambian Kwacha'],
      currencyFrom: '',
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
    handler: function () {
      const customWin = new BrowserWindow({ show: false })
      customWin.loadURL('https://www.google.com/search?q=bdt+to+yen')
      customWin.webContents.on('did-finish-load', () => {
        // const code = 'a = document.getElementByClassName('iBp4i');'
        // eslint-disable-next-line quotes
        customWin.webContents.executeJavaScript(`document.getElementsByClassName('b1hJbf')[0].attributes[1].nodeValue`, function (result) {
          this.someText = result
          console.log(result)
          console.log(this.someText)
        })
        // console.log(a)
      })
    }
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>
  .no-outline {
    outline: 0!important;
  }
</style>
