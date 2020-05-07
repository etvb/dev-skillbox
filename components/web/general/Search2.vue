<template>
  <div id="search">
    <b-navbar>
      <template slot="start">
        <div class="button-search">
          <select id="" @change="prueba2($event)" name="fs">
            <option value="1">
              uno
            </option>
            <option value="2">
              dos
            </option>
          </select>
        </div>
        <div class="button-search">
          <i class="fas fa-globe" />
          <span>Language</span>

          <b-field>
            <b-select
              v-model="search"                           
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
              <option value="other">
                Other languages
              </option>
            </b-select>
          </b-field>
        </div>
        
        <!-- button-Availability -->
        <b-dropdown aria-role="list">
          <button slot="trigger" slot-scope="{ active }" class="button is-primary2 mySize">
            <b-icon icon="account-multiple" />
            <span>Availability</span>
            <b-icon :icon="active ? 'menu-up' : 'menu-down'" />
            <p />
          </button>
          <b-dropdown-item aria-role="listitem">
            <div
              v-for="day in days"
              :key="day.id"
              class="field"
            >
              <b-checkbox
                v-model="daysChecked"
                :native-value="day.id"
              >
                {{ day.name }}
              </b-checkbox>
            </div>
          </b-dropdown-item>
        </b-dropdown>
        <!-- button-Speaker -->
        <b-dropdown on-change="prueba2($event)" aria-role="list">
          <button slot="trigger" slot-scope="{ active }" class="button is-primary2 mySize moreSpeaker ">
            <b-icon icon="account-multiple" />
            <span>Native Speaker</span>
            <b-icon :icon="active ? 'menu-up' : 'menu-down'" />
            <p>lsdk</p>
          </button>
          <b-dropdown-item aria-role="listitem">
            Action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Another action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem" class="prueba">
            Something else
          </b-dropdown-item>
        </b-dropdown>
        <!-- button-Price -->
        <b-dropdown aria-role="list">
          <button slot="trigger" slot-scope="{ active }" class="button is-primary2 mySize morePrice">
            <b-icon icon="account-multiple" />
            <span>Lesson Price</span>
            <b-icon :icon="active ? 'menu-up' : 'menu-down'" />
            <p>lsdk</p>
          </button>
          <b-dropdown-item aria-role="listitem">
            Action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Another action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Something else
          </b-dropdown-item>
        </b-dropdown>
        <!-- button-Location -->
        <b-dropdown aria-role="list">
          <button slot="trigger" slot-scope="{ active }" class="button is-primary2 mySize">
            <b-icon icon="account-multiple" />
            <span>Location</span>
            <b-icon :icon="active ? 'menu-up' : 'menu-down'" />
            <p>lsdk</p>
          </button>
          <b-dropdown-item aria-role="listitem">
            Action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Another action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Something else
          </b-dropdown-item>
        </b-dropdown>
        <!-- button-Rating -->
        <b-dropdown aria-role="list">
          <button slot="trigger" slot-scope="{ active }" class="button is-primary2 mySize lessRating">
            <b-icon icon="account-multiple" />
            <span>Rating</span>
            <b-icon :icon="active ? 'menu-up' : 'menu-down'" />
            <p>lsdk</p>
          </button>
          <b-dropdown-item aria-role="listitem">
            Action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Another action
          </b-dropdown-item>
          <b-dropdown-item aria-role="listitem">
            Something else
          </b-dropdown-item>
        </b-dropdown>
      </template>
    </b-navbar>
  </div>
</template>
<style lang="sass" scoped>
  #search
    background-color: white;
    margin-bottom: 1em 
    position: -webkit-sticky;
    position: sticky;
    top: 0;
    z-index: 10
  @media screen and (min-width: 1024px)
    #search nav .navbar-menu
      justify-content: center
    #search nav .navbar-menu .navbar-start
      margin-right: 0
    #search nav .navbar-menu .navbar-end
      margin-left: 0
  .button-search
    border: 1px solid lightgrey
  .button-search .fiel .control span select
    border: 0
  .mySize
    width: 150px;
    flex-wrap: wrap;
    height: 55px;
  .moreSpeaker, .morePrice
    width: 180px
  
  .lessRating
    width: 120px
</style>

<script>
import axios from 'axios'

export default {
  props: {
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
      prueba: '',
      search: '',
      languages: [],
      days: [
        { name: 'Sunday', id: 0 },
        { name: 'Monday', id: 1 },
        { name: 'Tuesday', id: 2 },
        { name: 'Wednesday', id: 3 },
        { name: 'Thursday', id: 4 },
        { name: 'Friday', id: 5 },
        { name: 'Saturday', id: 6 }
      ],
      loading: false
    }
  },
  computed: {
    lenguaje() {
      const id = parseInt(this.search)
      // eslint-disable-next-line no-console
      console.log('id' + id)
      return this.languages.find(language => {
        return language.id === id
      })
    }
  },
  mounted() {
    this.delete()
    this.setLanguages()
    if (this.selected) {
      this.search = this.selected
    }
  },
  methods: {
    prueba2(event) {
      // eslint-disable-next-line no-console
      console.log(event)
    },
    delete() {
      const border = document.querySelectorAll('select')
      for (const item of border) {
        item.style.border = 0
      }
    },
    searchInstructors() {
      // eslint-disable-next-line no-console
      console.log('hola')
      if (this.search === '') {
        alert('Please select a language')
        return
      }
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1000)
      const days = this.getDaysFiltereds()
      const rangePrice = this.getRangePrice()
      // this.$router.push('/' + this.search + '/instructors')
      this.$router.push('/' + this.search + '/instructors?' + days + rangePrice)
    },
    setLanguages() {
      // const url = process.env.apiUrl + 'languages'
      const url = process.env.apiUrl + 'languages/availables'
      axios.get(url).then(response => {
        this.languages = response.data
        // eslint-disable-next-line no-console
      })
    },
    getDaysFiltereds() {
      const days = this.daysChecked
      if (!days.length) return ''

      return 'days=' + days
    },
    getRangePrice() {
      const range = this.range
      return '&price=' + range[0] + '-' + range[1]
    }
  }
}
</script>
