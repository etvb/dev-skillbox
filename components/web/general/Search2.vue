<template>
  <div id="navbar-web2 search">
    <div>
      <nav class="navbar2" role="navigation" aria-label="main navigation">
        <div class="navbar-brand">
          <!-- nuxt-imagen -->
          <!-- start button hamburger -->
          <div
            @click="openMenu2"
            role="button"
            class="navbar-burger burger"
            aria-label="menu"
            aria-expanded="false"
            data-target2="navbar2"
          >
            <span aria-hidden="true" />
            <span aria-hidden="true" />
            <span aria-hidden="true" />
          </div>
          <!-- end button hamburger -->
        </div>
        <div id="navbar2" class="navbar-menu">
          <!-- aqui poner los botones -->


          <!--start buttom language -->
          <!-- <div class="button-search-pink"> -->
          <!-- <i class="fas fa-globe" /> -->
          <!-- {{ search }} -->
          <b-field class="field">
            <span class="titleButtom">Language</span>
            <!-- :input="searchInstructors()" -->
            <select
              v-model="search"
              @change="changeLanguage(search)"
              class="searchSelect-pink pointer"
            >
              <option
                v-for="language in languages"
                :value="language.id"
                :key="language.id"
              >
                &nbsp;&nbsp;{{ language.english }}
              </option>
              <option value="others">
                &nbsp;&nbsp;Other languages
              </option>
            </select>
            <i class="fas fa-angle-down arrow" />
          </b-field>
          <!-- </div> -->
          <!--end buttom language -->

          <!-- button-Availability -->
          <div @click="showMe()" :class="[daysComponent.length !== 0 ? used='used' : '']" class="button-search pointer">
            <!-- <i class="far fa-calendar-alt" /> -->

            <span class="titleButtom2">Availability</span>
            <br>
            <div class="lineHige">
              <!-- {{ daysComponent }} -->
              <span id="su" class="sizeSmall has-text-weight-bold colorDays">Su</span>
              <span id="mo" class="sizeSmall has-text-weight-bold colorDays">Mo</span>
              <span id="tu" class="sizeSmall has-text-weight-bold colorDays">Tu</span>
              <span id="we" class="sizeSmall has-text-weight-bold colorDays">We</span>
              <span id="th" class="sizeSmall has-text-weight-bold colorDays">Th</span>
              <span id="fr" class="sizeSmall has-text-weight-bold colorDays">Fr</span>
              <span id="sa" class="sizeSmall has-text-weight-bold colorDays">Sa</span>
              <i class="fas fa-angle-down" />
            </div>
            <div id="menu" class="days">
              <div
                v-for="day in days"
                :key="day.id"
                class="field"
              >
                <!-- <b-checkbox
                  v-model="daysChecked"
                  :native-value="day.id"
                  :input="searchInstructors()"
                >
                  {{ day.name }}
                </b-checkbox> -->
                <b-checkbox
                  v-model="daysComponent"
                  :native-value="day.id"
                  @input="changeDays(day.id)"
                >
                  {{ day.name }}
                </b-checkbox>
              </div>
            </div>
          </div>
          <!-- end button-Availability -->

          <!-- button-Speaker -->
          <!-- <div class="button-search-pink"> -->
          <!-- <i class="fas fa-chalkboard-teacher" /> -->
          <b-field class="field">
            <span class="titleButtom">Native Speaker</span>
            <div id="NO">
              No
            </div>
            <!-- if you want disable the native speaker button, put this like a param= :disabled="disableNative" -->
            <select
              v-model="native"
              @change="changeNativeSpeaker(native)"
              class="searchSelect-pink pointer"
            >
              <option value="1">
                &nbsp;&nbsp;Yes
              </option>
              <option value="0" selected="selected">
                &nbsp;&nbsp;No
              </option>
            </select>
            <i class="fas fa-angle-down arrow" />
          </b-field>
          <!-- </div> -->
          <!--end button-Speaker -->

          <!-- Lesson Price -->
          <b-field :class="[range[1] !== '0' ? used='used' : '']" class="button-search">
            <span class="titleButtom2">Lesson Price</span>
            <div class="contentNumber">
              <vue-slider
                v-model="range[1]"
                :tooltip="'always'"
                :tooltip-placement="['bottom']"
                @change="changeRangePrice"
                
                :min="min"
                :max="max"
              /> 

                
              <!-- fin slide -->
            </div>
            <!-- </div> -->
          </b-field>
          <!--end Lesson Price -->

          <!-- localtion -->
          <!-- <div :class="[locationSelected !== '' ? used ='used': '', ]" class="button-search"> -->
          <!-- <i class="fas fa-chalkboard-teacher" /> -->
          <b-field class="field">
            <span class="titleButtom">Location</span>
            <select
              v-model="locationSelected"
              @change="changeLocation(locationSelected)"
              :class="[locationSelected !== '' ? used='used' : '']"
              class="searchSelect pointer"
            >
              <option value="">
                &nbsp;&nbsp;All
              </option>
              
              <option
                v-for="$location in locationes"
                :key="$location"
                :value="$location"
              >
                &nbsp;&nbsp;{{ $location }}
              </option>
            </select>
            <i class="fas fa-angle-down arrow" />
          </b-field>
          <!-- </div> -->
          <!--end localtion -->

          <!-- rating -->
          
          <!-- <i class="fas fa-chalkboard-teacher" /> -->

          <b-field class="field">
            <span class="titleButtom">Rating</span>
            <select
              v-model="rating"
              @change="changeRating(rating)"
              :class="[rating !== '' ? used='used' : '']"
              class="searchSelect pointer"
            >
              <!-- :expanded="true"
                placeholder=""
                size="is-small" -->
              <option value="">
                &nbsp;&nbsp;All
              </option>
              <option value="1">
                &nbsp;&nbsp;*
              </option>
              <option value="2">
                &nbsp;&nbsp;* *
              </option>
              <option value="3">
                &nbsp;&nbsp;* * *
              </option>
              <option value="4">
                &nbsp;&nbsp;* * * *
              </option>
            </select>
            <i class="fas fa-angle-down arrow" />
          </b-field>
          <!--end rating -->
        </div>
      </nav>
    </div>
  </div>
</template>
<style lang="sass" scoped>

  .navbar-menu
    line-height: normal

  .lineHige
    // line-height: 1

  select option
    background-color: white
    -moz-background-color: white
    text-align: center
    

  .pointer
    cursor: pointer
    &:hover
      box-shadow: 0 10px 8px rgba(0, 0, 0, 0.15), 0 1px 10px rgba(0, 0, 0, 0.2)

  select:focus
    outline:none !important

  .used
    background-color: #ffc0cbb3 !important
    border: 3px solid #df4661 !important 
  // #fb05bb
  .searchSelect, .searchSelect-pink

    text-align: center
    padding-top: 20px
    border: 1px solid lightgrey
    // display: inline-block
    // height: 55px
    border-radius: 10px
    // min-width: 150px
    // cursor: pointer
    // background-color: white
    font-family: calibri  
    text-align-last: center
    background-color: white
    min-width: 160px
    height: 50px
    appearance: none
    -webkit-appearance: none
    // padding-left: 8px
    border-color: #dbdbdb
    border-width: 2px
    border-style: solid
    color: darkgrey
    // font-weight: bold
    font-size: 18px
  .searchSelect-pink
    background-color: #ffc0cbb3
    border-color: #df4661
    border-width: 3px


  .field
    margin: 0 5px 5px 5px
    position: relative
    display: inline-block
  .arrow
    position: absolute
    top: 30px
    left: 143px
    z-index: 10
    pointer-events: none
  .colorDays
    color: #df4661
  #NO
    font-family: calibri 
    font-size: 18px
    pointer-events: none
    position: absolute
    z-index: 1
    margin-top: 22px
    margin-left: 74px
    // font-family: 'sans-serif'
    // font-size: 13px
    color: darkgrey
    // font-weight: bold
  i.fas,
  i.far
    color: hsl(204, 86%, 53%)
  .fa-angle-down
    color: #df4661 !important
  .navbar-menu2
    // background-color: #f5f9fc
    // height: 80px
    // width: 100%
    display: flex
    justify-content: center
    align-items: center
    flex-wrap: wrap
    // background-color: #34495e
  #navbar2
    justify-content: center
    margin-bottom: 1rem
  #search
    background-color: #f5f9fc;
    margin-bottom: 1em
    position: -webkit-sticky;
    position: sticky;
    top: 0;
    z-index: 10
  .days
    width: 150px
    border: 1px solid lightgrey
    position: absolute
    top: 120px
    background-color: white
    padding: 3px
    display: none
    z-index: 20
    text-align: initial;
  @media screen and (min-width: 230px)
    .days
      top: 120px
  // @media screen and (min-width: 373px)
  //   .days
  //     top: 120px

  .days.show
    display: block
  .sizeSmall
    margin-top: 5px
    font-size: 10px
  @media screen and (min-width: 1024px)
    #search nav .navbar-menu
      line-height: normal
      font-family: calibri 
      font-size: 18px
      justify-content: center
    #search nav .navbar-menu .navbar-start
      margin-right: 0
    #search nav .navbar-menu .navbar-end
      margin-left: 0
  .button-search, 
  .button-search-pink
    text-align: center
    padding: 0 5px
    margin: 0 5px 5px 5px
    border: 2px solid lightgrey
    display: inline-block
    height: 50px
    border-radius: 10px
    min-width: 160px
    // cursor: pointer
    background-color: white
  .button-search-pink
    background-color: #ffc0cbb3
    border-color: #fb05bb


  .button-search .fiel .control span select
    border: 0
  .titleButtom, .titleButtom2
    font-family: calibri 
    font-size: 18px
    color: black
    // font-size: 14px
    font-weight: bold
    width: 100%
    text-align-last: center
    pointer-events: none
  .titleButtom
    position: absolute
    margin-top: 3px
    
  .mySize
    width: 150px;
    flex-wrap: wrap;
    height: 55px;
  .moreSpeaker, .morePrice
    width: 180px

  .lessRating
    width: 120px
  .contentNumber
    display: grid
    text-align: center
    font-family: calibri 
    font-size: 18px
  .sizeNumber
    width: 137px
    height: 24px
</style>

<script>
import axios from 'axios'
import VueSlider from 'vue-slider-component/dist-css/vue-slider-component.umd.min.js'
import 'vue-slider-component/dist-css/vue-slider-component.css'

export default {
  components: {
    VueSlider
  },
  props: {
    // search: {
    //   type: String,
    //   default: ''
    // },
    dataPrueba: {
      type: Object,
      default: () => {}
    },
    countryPasada: {
      type: String,
      default: ''
    },
    selected: {
      type: String,
      default: ''
    },
    daysFilter: {
      type: Boolean,
      default: false
    },
    daysChecked: {
      type: Array,
      default: () => []
    },
    rangeFilter: {
      type: Boolean,
      default: false
    },
    range: {
      type: Array,
      default: () => [0, 50]
    }
  },
  data() {
    return {
      marks: [0, 50],
      usado: true,
      disableNative: false,
      min: 0,
      max: 50,
      native: '',
      rating: '',
      locationSelected: '',
      locationes: [],
      // prueba: 0,
      search: '',
      languages: '',
      days: [
        { name: 'Sunday', id: 0 },
        { name: 'Monday', id: 1 },
        { name: 'Tuesday', id: 2 },
        { name: 'Wednesday', id: 3 },
        { name: 'Thursday', id: 4 },
        { name: 'Friday', id: 5 },
        { name: 'Saturday', id: 6 }
      ],
      loading: false,
      daysComponent: this.daysChecked.slice()
    }
  },
  // computed: {
  //   lenguaje() {
  //     const id = parseInt(this.search)
  //     // eslint-disable-next-line no-console
  //     console.log('id' + id)
  //     return this.languages.find(language => {
  //       return language.id === id
  //     })
  //   }
  // },
  // whit this no error alert, this is called firt
  beforeMount() {
    if (this.selected) {
      this.search = this.selected
    }
    if (this.dataPrueba.instructors) {
      this.locationsFunctionInstructors()
    } else {
      this.locationFunctionOther()
    }
  },
  mounted() {
    this.changeColorVueSlider()
    this.setLanguages()
    // this.changeColorDays()
    // this.locationsFunction()
    // this.getLocation()
    // eslint-disable-next-line no-console
    // console.log(this.range)
    if (this.search === 'others') {
      this.disableNative = true
    }
  },
  methods: {
    changeColorVueSlider() {
      const vueSliderProcess = document.getElementsByClassName(
        'vue-slider-process'
      )
      const tooltip = document.getElementsByClassName(
        'vue-slider-dot-tooltip-inner'
      )
      const vueSliderRail = document.getElementsByClassName('vue-slider-rail')
      vueSliderProcess[0].style.backgroundColor = '#df4661'
      vueSliderRail[0].style.backgroundColor = '#df4661'
      tooltip[0].style.backgroundColor = '#ffc0cbb3'
      tooltip[0].style.borderColor = '#ffc0cbb3'
      tooltip[0].style.color = 'black'
      tooltip[0].style.fontSize = '11px'
      tooltip[0].style.padding = 0
    },
    changeColorDays(dia) {
      switch (dia) {
        case 0:
          const sunday = document.getElementById('su')
          sunday.classList.toggle('colorDays')
          break
        case 1:
          const monday = document.getElementById('mo')
          monday.classList.toggle('colorDays')
          break
        case 2:
          const tuesday = document.getElementById('tu')
          tuesday.classList.toggle('colorDays')
          break
        case 3:
          const wednesday = document.getElementById('we')
          wednesday.classList.toggle('colorDays')
          break
        case 4:
          const thurday = document.getElementById('th')
          thurday.classList.toggle('colorDays')
          break
        case 5:
          const friday = document.getElementById('fr')
          friday.classList.toggle('colorDays')
          break
        case 6:
          const saturday = document.getElementById('sa')
          saturday.classList.toggle('colorDays')
      }
    },
    openMenu2(event) {
      const element = event.target
      const trigger = element.closest('div')

      const target = trigger.dataset.target2
      const $target = document.getElementById(target)

      trigger.classList.toggle('is-active')
      $target.classList.toggle('is-active')
    },
    showMe() {
      const menu = document.getElementById('menu')
      menu.classList.toggle('show')
    },
    delete() {
      const border = document.querySelectorAll('select')
      for (const item of border) {
        item.style.border = 0
      }
    },
    /* searchInstructors() {
      // eslint-disable-next-line no-console
      console.log('ejecutando desde SE2')
      // if (this.search === '') {
      //   alert('Please select a language5')
      //   return
      // }
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1000)
      const days = this.getDaysFiltereds()
      const rangePrice = this.getRangePrice()
      const locationes = this.getLocation()
      // this.$router.push('/' + this.search + '/instructors')
      // this.$router.push(
      //   '/' + this.search + '/instructors?' + days + rangePrice + locationes
      // )
      this.$router.push(
        `/${this.search}/instructors?${days +
          rangePrice +
          locationes}&test='33ss'`
      )
    }, */
    setLanguages() {
      // const url = process.env.apiUrl + 'languages'
      const url = process.env.apiUrl + 'languages/availables'
      axios.get(url).then(response => {
        this.languages = response.data
        // eslint-disable-next-line no-console
      })
    },
    /* getDaysFiltereds() {
      const days = this.daysChecked
      // si esta vacio devuelve el arreglo vacio
      if (!days.length) return ''

      return 'days=' + days
    }, */
    getRangePrice() {
      const range = this.range
      return '&price=' + range[0] + '-' + range[1]
    },
    /* getLocation() {
      const location = this.locationSelected
      // eslint-disable-next-line no-console
      console.log(location)
      return '&location=' + location
    }, */
    locationsFunctionInstructors() {
      const instructors = this.dataPrueba.instructors
      const locations = []
      instructors.forEach(element => {
        if (
          locations.indexOf(element.user.country) === -1 &&
          element.user.country !== null
        ) {
          locations.push(element.user.country)
        }
      })
      this.locationes = locations
    },
    locationFunctionOther() {
      const instructors = this.dataPrueba
      const locations = []
      instructors.forEach(element => {
        element.instructors.forEach(element => {
          if (
            locations.indexOf(element.user.country) === -1 &&
            element.user.country !== null
          ) {
            locations.push(element.user.country)
          }
        })
      })
      this.locationes = locations
    },
    changeNativeSpeaker(value) {
      this.hideNO()
      this.$router.push({
        path: this.$route.fullPath,
        query: { native: value }
      })
    },
    hideNO() {
      // add 'NO' in the buttom native spiker
      const element = document.getElementById('NO')
      element.style.display = 'none'
    },
    changeDays(dia) {
      this.$emit('changeDays', this.daysComponent)
      this.changeColorDays(dia)
    },
    changeLocation(value) {
      this.$router.push({
        path: this.$route.fullPath,
        query: { location: value }
      })
    },
    changeRating(value) {
      this.$router.push({
        path: this.$route.fullPath,
        query: { rating: value }
      })
    },
    changeLanguage(value) {
      // this.$emit('prueba', value)
      // eslint-disable-next-line no-console
      // console.log('YE ESTRE')
      // eslint-disable-next-line no-console
      // console.log(value)
      // this.$router.push('/' + this.search + '/instructors')
      // const path = this.$route.fullPath
      // const newPath = path.replace(this.selected, value)
      // this.$router.push({
      //   path: newPath
      // })
      // this.changeRating()
      // this.$router.pa
      // this.$route.params.lang = this.search
      // otra forma de hacerlo
      this.$router.push({
        path: '/' + value + '/instructors',
        query: {
          days: '0,1,2,3,4,5,6'
        }
      })
    },
    changeRangePrice() {
      // const price = this.range[0] + '-' + this.range[1]
      this.$router.push({
        path: this.$route.fullPath,
        query: { price: this.range[0] + '-' + this.range[1] }
      })
    }
  }
}
</script>
