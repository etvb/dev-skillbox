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
          <div class="button-search">
            <i class="fas fa-globe" />
            <span class="titleButtom">Language</span>
            <!-- {{ search }} -->
            <b-field>
              <!-- :input="searchInstructors()" -->
              <b-select
                v-model="search"
                @input="changeLanguage"
                placeholder="Select language"
                size="is-small"
              >
                <option
                  v-for="language in languages"
                  :value="language.id"
                  :key="language.id"
                >
                  {{ language.english }}
                </option>
                <option value="others">
                  Other languages
                </option>
              </b-select>
            </b-field>
          </div>
          <!--end buttom language -->

          <!-- button-Availability -->
          <div @click="showMe()" class="button-search">
            <i class="far fa-calendar-alt" />

            <span class="titleButtom">Availability</span>
            <br>
            <div>
              <!-- {{ daysChecked }} -->
              <span class="sizeSmall">Su</span>
              <span class="sizeSmall">Mo</span>
              <span class="sizeSmall">Tu</span>
              <span class="sizeSmall">We</span>
              <span class="sizeSmall">Th</span>
              <span class="sizeSmall">Fr</span>
              <span class="sizeSmall">Sa</span>
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
                  :input="changeDays()"
                >
                  {{ day.name }}
                </b-checkbox>
              </div>
            </div>
          </div>
          <!-- end button-Availability -->

          <!-- button-Speaker -->
          <div class="button-search">
            <i class="fas fa-chalkboard-teacher" />
            <span class="titleButtom">Native Speaker</span>

            <b-field>
              <b-select
                v-model="native"
                @input="changeNativeSpeaker"
                size="is-small"
                expanded="true"
              >
                <option value="1">
                  YES
                </option>
                <option value="0" selected>
                  NO
                </option>
              </b-select>
            </b-field>
          </div>
          <!--end button-Speaker -->

          <!-- Lesson Price -->
          <div class="button-search">
            <i class="far fa-money-bill-alt" />
            <span class="titleButtom">Lesson Price</span>
            <div>
              <!-- <i class="fas fa-angle-down" /> -->
              <div class="contentNumber">
                <input
                  v-model="range[0]"
                  :max="range[1]"
                  @change="changeRangePrice"
                  class="sizeNumber"
                  type="number"
                  placeholder="Min 0"
                  min="0"
                >
                <input
                  v-model="range[1]"
                  :min="range[0]"
                  @change="changeRangePrice"
                  class="sizeNumber"
                  type="number"
                  placeholder="Max 50"
                  max="50"
                >
              </div>
            </div>
          </div>
          <!--end Lesson Price -->

          <!-- localtion -->
          <div class="button-search">
            <i class="fas fa-chalkboard-teacher" />
            <span class="titleButtom">Location</span>

            <b-field>
              <b-select
                v-model="locationSelected"
                @input="changeLocation"
                placeholder=""
                size="is-small"
              >
                <option
                  v-for="($location ) in locationes"
                  :key="$location"
                >
                  {{ $location }}
                </option>
              </b-select>
            </b-field>
          </div>
          <!--end localtion -->

          <!-- rating -->
          <div class="button-search">
            <i class="fas fa-chalkboard-teacher" />
            <span class="titleButtom">Rating</span>

            <b-field>
              <b-select
                v-model="rating"
                @input="changeRating"
                expanded="true"
                placeholder=""
                size="is-small"
                class="prueba"
              >
                <option value="0">
                  *
                </option>
                <option value="2">
                  * *
                </option>
                <option value="3">
                  * * *
                </option>
                <option value="4">
                  * * * *
                </option>
              </b-select>
            </b-field>
          </div>
          <!--end rating -->
        </div>
      </nav>
    </div>
  </div>
</template>
<style lang="sass" scoped>
  .navbar-menu2
    // background-color: #f5f9fc
    // height: 80px
    // width: 100%
    display: flex
    justify-content: center
    align-items: center
    flex-wrap: wrap
    // background-color: #34495e
  #search
    background-color: #f5f9fc;
    margin-bottom: 1em
    position: -webkit-sticky;
    position: sticky;
    top: 0;
    z-index: 10
  .days
    border: 1px solid lightgrey
    position: absolute
    top: 120px
    background-color: white
    padding: 3px
    display: none
    z-index: 10
  @media screen and (min-width: 230px)
    .days
      top: 160px
  @media screen and (min-width: 373px)
    .days
      top: 120px

  .days.show
    display: block
  .sizeSmall
    margin-top: 5px
    font-size: 10px
  @media screen and (min-width: 1024px)
    #search nav .navbar-menu
      justify-content: center
    #search nav .navbar-menu .navbar-start
      margin-right: 0
    #search nav .navbar-menu .navbar-end
      margin-left: 0
  .button-search
    padding: 0 5px
    margin: 0 5px 5px 5px
    border: 1px solid lightgrey
    display: inline-block
    height: 55px
    border-radius: 10px
    min-width: 150px
    cursor: pointer
    background-color: white
  .button-search .fiel .control span select
    border: 0
  .titleButtom
    font-size: 14px
    font-weight: bold
  .mySize
    width: 150px;
    flex-wrap: wrap;
    height: 55px;
  .moreSpeaker, .morePrice
    width: 180px

  .lessRating
    width: 120px
  .contentNumber
    text-align: center
  .sizeNumber
    width: 62px
    height: 22px
</style>

<script>
import axios from 'axios'

export default {
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
      min: '',
      max: '',
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
    // this.delete()
    this.setLanguages()
    // eslint-disable-next-line no-console
    console.log('ROUTE')
    // this.locationsFunction()
    // this.getLocation()
    // eslint-disable-next-line no-console
    console.log(this.$route)
  },
  methods: {
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
    prueba2() {
      // eslint-disable-next-line no-console
      console.log('llamada')
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
      this.$router.push({
        path: this.$route.fullPath,
        query: { native: value }
      })
    },
    changeDays() {
      this.$emit('changeDays', this.daysComponent)
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
        query: { rating: this.rating, native: this.native }
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
