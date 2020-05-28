<template>
  <div class="section">
    <div class="container">
      <!-- navbar -->
      <search2
        :selected="selectedLang"
        :daysChecked="daysChecked"
        :range="range"
        :mostrar="false"
        :countryPasada="countryParaPasar"
        :dataPrueba="infoInstructors"
        :prueba="language"
        @changeDays="changeDays"
        @prueba="infoComponente"
      />

      <h4 v-if="language.instructors" class="title is-4 has-text-centered">
        We've  found {{ language.instructors.length }} teachers
      </h4>
      <h4 v-else class="title is-4 has-text-centered">
        We've  found {{ totalInstructors }} teachers
      </h4>
      <div class="columns">
        <div class="column is-4">
          <div>
            <search
              :selected="selectedLang"
              :daysFilter="true"
              :rangeFilter="true"
              :daysChecked="daysChecked"
              :range="range"
            />
          </div>
        </div>
        <div v-if="language.instructors" class="column">
          <div
            v-for="(instructor, index) in language.instructors"
            v-if="instructor.user"
            :key="instructor.id"
          >
            <!-- <nuxt-link
            :to="'/'+$route.params.lang+'/instructors/' + instructor.id"
            v-for="(instructor, index) in language.instructors"
            v-if="instructor.user"
            :key="instructor.id"
          > -->
            <div
              :class="index != 0 ? '-is-spaced-top': ''"
              class="box is-radiusless -card-vertical container-profile "
            >
              <div class="container-profile-info">
                <!-- changed the img tag fot div, if the user has image show  -->
                <div
                  v-if="instructor.user.profile_picture"
                  :style="'background-image: url(' + instructor.user.profile_picture + '); background-size: cover; background-repeat: no-repeat'"
                  class="-is-circle -profile-picture is-inline-block"
                />
                
                <!-- if the user don´t have imege show this -->
                <img
                  v-else
                  style="opacity: .2;"
                  src="/profile.png"
                  class="-is-circle -profile-picture"
                >
                <!-- <div v-else class="-profile-picture is-inline-block" /> -->
                <div class="container-profile-main">
                  <div class="container-profile-name">
                    <h5 class="title is-marginless is-6 has-text-weight-bold">
                      {{ instructor.user.name + ' ' + instructor.user.lastname[0] + '.' }}
                    </h5>
                    <span class="container-profile-flag">BAndera</span>
                  </div>
                  <p class="has-text-grey-lighter has-text-weight-semibold"> Native Language: <span>{{ instructor.user.language.english }}</span> </p><br>
                  <p class="container-profile-raiting has-text-grey-lighter has-text-weight-semibold">
                    Raiting: <rating :rating="instructor.average_rating ? instructor.average_rating : 0" />
                  </p>
                </div>
                <div>
                  <like />
                </div>
              </div>
              <hr>
              <div class="is-inline-block -description container-profile-description">
                <p class="subtitle is-6 profile-description">
                  {{ instructor.description | truncate(180) }}  
                  <nuxt-link
                    :to="'/'+$route.params.lang+'/instructors/' + instructor.id"
                  >
                    <span class="has-text-weight-bold has-text-info	"> read more.</span> 
                  </nuxt-link>
                </p>
              </div>
              <hr>
              <div class="container-profile-teacher">
                <!-- <b-tag class="is-rounded -top-badge">
                  &nbsp; Top &nbsp;
                </b-tag>
                <rating :rating="instructor.average_rating ? instructor.average_rating : 0" class="is-pulled-right" /> -->
                <div>
                  <p class="is-size-7 has-text-grey-lighter has-text-weight-bold">Lesson Price:</p>
                  <p class="has-text-weight-semibold"> USD {{ instructor.price_by_class }} </p>
                  <button class="button is-info is-expand is-fullwidth">
                    Book
                  </button>
                </div>
                <div>
                  <p class="is-size-7 has-text-grey-lighter has-text-weight-bold">Location:</p>
                  <p class="has-text-weight-semibold">{{ instructor.user.country }}</p>
                  <nuxt-link
                    :to="'/'+$route.params.lang+'/instructors/' + instructor.id"
                  > 
                    <button class="button is-info is-expand is-fullwidth">
                      Schedule
                    </button>
                  </nuxt-link>
                </div>
                <div>
                  <p class="is-size-7 has-text-grey-lighter has-text-weight-bold">Teaches:</p>
                  <p class="has-text-weight-semibold">put lengugages</p>
                  <button class="button is-info is-expand is-fullwidth">
                    Video
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div v-else class="column">
          <template v-for="(lang, indexLang) in language">
            <nuxt-link
              :to="'/'+lang.id+'/instructors/' + instructor.id"
              v-for="(instructor, index) in lang.instructors"
              v-if="instructor.user"
              :key="instructor.id"
              :class="indexLang != 0 ? '-is-spaced-top': ''"
              class="is-block"
            >
              <div
                :class="index != 0 ? '-is-spaced-top': ''"
                class="box is-radiusless -card-vertical"
              >
                <div>
                  <img
                    v-if="instructor.user.profile_picture"
                    :src="instructor.user.profile_picture"
                    class="-is-circle -profile-picture"
                  >
                  <div v-else class="-profile-picture is-inline-block" />
                  <div class="is-inline-block -description">
                    <h5 class="title is-6 is-marginless">
                      {{ instructor.user.name + ' ' + instructor.user.lastname[0] + '.' }}
                    </h5>
                    <h5 class="title is-6">
                      {{ lang.english }}
                    </h5>
                    <p class="subtitle is-6">
                      {{ instructor.description }}
                    </p>
                  </div>
                </div>
                <hr>
                <div class="">
                  <b-tag class="is-rounded -top-badge">
                    &nbsp; Top &nbsp;
                  </b-tag>
                  <rating :rating="instructor.average_rating ? instructor.average_rating : 0" class="is-pulled-right" />
                </div>
              </div>
            </nuxt-link>
          </template>
        </div>
        <!-- <div class=" column is-2" /> -->
      </div>
    </div>
  </div>
</template>
<style lang="sass">

  hr
    margin-top: 10px
  rating
    float: none !important
  .container-card
    
  .container-profile
    // border: 2px solid red
    padding-left: 30px
    padding-right: 30px
  
  .container-profile-main
    flex: 1 1 auto
    margin-left: 20px
    margin-right: 20px

  .container-profile-info, 
  .container-profile-name,
  .container-profile-teacher
    display: flex
    justify-content: space-between 

  .container-profile-raiting
    margin-top: -25px
  
  .container-profile-flag
    margin-right: 10px

  .container-profile-description
    min-height: 60px
    .profile-description
      margin-left: 30px
      margin-right: 30px

  // .container-profile-name
  //   flex: 1 1 auto

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
  .mySize
    width: 150px;
    flex-wrap: wrap;
    height: 55px;
  .moreSpeaker, .morePrice
    width: 180px

  .lessRating
    width: 120px
  .mybg
    background-color: #f5f9fc;

  .-card-vertical
    .-profile-picture
      margin-right: 1rem
      height: 60px
      width: 60px
    .-description
      vertical-align: super
    &:hover
      // cursor: pointer
      box-shadow: 0 10px 8px rgba(0, 0, 0, 0.15), 0 1px 10px rgba(0, 0, 0, 0.2)
</style>

<script>
import Like from '~/components/general/Like.vue'
import Search from '~/components/web/general/Search.vue'
import Search2 from '~/components/web/general/Search2.vue'
import Rating from '~/components/web/general/Rating.vue'
import axios from 'axios'
export default {
  components: {
    Like,
    Search,
    Search2,
    Rating
  },
  // watchQuery: ['days', 'price', 'country', 'native'],
  watchQuery: true,
  filters: {
    truncate: function(value, limit) {
      // eslint-disable-next-line no-console
      // console.log(value)
      if (String(value).length > limit) {
        value = value.substring(0, limit - 3) + '... '
      }

      return value
    }
  },
  data() {
    return {
      selectedLang: this.$route.params.lang,
      language: {
        instructors: []
      },
      totalInstructors: 0,
      // daysChecked: [],
      range: []
      // prueba: {}
      // countryParaPasar: []
    }
  },
  async asyncData({ params, query }) {
    // eslint-disable-next-line no-console
    console.log('ya entre')

    const langId = params.lang
    let days = ['0', '1', '2', '3', '4', '5', '6']
    let range = [0, 50]
    let native = 0
    let rating = null
    let location = null
    // const location = ''
    // eslint-disable-next-line no-console
    console.log('ASYNC ' + query.location)
    if (query.days) {
      days = query.days.split(',')
    }
    if (query.price) {
      range = query.price.split('-')
    }
    if (query.native) {
      native = query.native
    }
    if (query.location) {
      location = query.location
    }
    if (query.rating) {
      rating = query.rating
    }

    const url = `${process.env.apiUrl}languages/${langId}/instructors`
    const filters = {
      days: days,
      price_range: range,
      country: location,
      native,
      rating,
      location
    }
    const { data } = await axios.post(url, filters)
    // eslint-disable-next-line no-console
    console.log('data de ESTE INDX')
    // eslint-disable-next-line no-console
    console.log(data.language)
    return {
      language: data.language,
      daysChecked: days,
      totalInstructors: data.totalInstructors,
      range,
      infoInstructors: data.language,
      countryParaPasar: location,
      native,
      location,
      rating
    }
  },
  methods: {
    changeDays(days = []) {
      this.daysChecked = days
      const newDays = days.toString()
      this.$router.push({
        path: this.$route.fullPath,
        query: { days: newDays }
      })
    },
    infoComponente(language) {
      // eslint-disable-next-line no-console
      console.log('dentro del PADRE')
      // eslint-disable-next-line no-console
      console.log(language)

      // this.$router.push({
      //   path: '/' + language + '/instructors/' + this.$router.query.rating
      // })
    }
  }
  // methods: {
  //   truncString(str, max, add) {
  //     // eslint-disable-next-line no-console
  //     console.log(this.language)
  //     add = add || '...'
  //     return typeof str === 'string' && str.length > max
  //       ? str.substring(0, max) + add
  //       : str
  //   }
  // }
}
</script>
