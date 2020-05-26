<template>
  <div class="section mybg">
    <div class="container">
      <!-- navbar -->
      <search2
        :selected="selectedLang"
        :daysFilter="true"
        :rangeFilter="true"
        :daysChecked="daysChecked"
        :range="range"
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
              class="box is-radiusless -card-vertical container-profile"
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
                    <h5 class="title is-marginless is-6">
                      {{ instructor.user.name + ' ' + instructor.user.lastname[0] + '.' }}
                    </h5>
                    <span class="container-profile-flag">BAndera</span>
                  </div>
                  <p>Native Language: <span>put languege</span> </p><br>
                  <p class="container-profile-raiting">Raiting: <rating :rating="instructor.average_rating ? instructor.average_rating : 0" /></p>
                </div>
                <div>
                  <span>Corazon
                  </span>
                  <like />
                </div>
              </div>
              <hr>
              <div class="is-inline-block -description">
                <p class="subtitle is-6">
                  {{ instructor.description | truncate(180) }}read more
                </p>
              </div>
              <hr>
              <div class="container-profile-teacher">
                <!-- <b-tag class="is-rounded -top-badge">
                  &nbsp; Top &nbsp;
                </b-tag>
                <rating :rating="instructor.average_rating ? instructor.average_rating : 0" class="is-pulled-right" /> -->
                <div>
                  <p>Lesson Price:</p>
                  <p>USD put $$$</p>
                  <button class="button is-info is-expand is-fullwidth">Book</button>
                </div>
                <div>
                  <p>Location:</p>
                  <p>put contry</p>
                  <nuxt-link
                    :to="'/'+$route.params.lang+'/instructors/' + instructor.id"
                  > 
                    <button class="button is-info is-expand is-fullwidth">Schedule</button>
                  </nuxt-link>
                </div>
                <div>
                  <p>Teaches:</p>
                  <p>put lengugages</p>
                  <button class="button is-info is-expand is-fullwidth">Video</button>
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
      </div>
    </div>
  </div>
</template>
<style lang="sass">

  hr
    margin-top: 10px
  rating
    float: none !important
  .container-profile
    border: 2px solid red
  
  .container-profile-main
    flex: 1 1 auto

  .container-profile-info, 
  .container-profile-name,
  .container-profile-teacher
    display: flex
    justify-content: space-between 

  .container-profile-raiting
    margin-top: -25px
  
  .container-profile-flag
    margin-right: 10px

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
      cursor: pointer
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
  watchQuery: ['days', 'price'],
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
      daysChecked: [],
      range: []
    }
  },
  async asyncData({ params, query }) {
    const langId = params.lang
    let days = ['0', '1', '2', '3', '4', '5', '6']
    let range = [0, 50]
    if (query.days) {
      days = query.days.split(',')
    }
    if (query.price) {
      range = query.price.split('-')
    }

    const url = `${process.env.apiUrl}languages/${langId}/instructors`
    const filters = {
      days: days,
      price_range: range
    }
    const { data } = await axios.post(url, filters)
    return {
      language: data.language,
      daysChecked: days,
      totalInstructors: data.totalInstructors,
      range
    }
  },
  methods: {
    // truncString(str, max, add) {
    //   add = add || '...'
    //   return typeof str === 'string' && str.length > max
    //     ? str.substring(0, max) + add
    //     : str
    // }
  }
}
</script>
