<template>
  <div class="section mybg">
    <div class="container">
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
          <nuxt-link
            :to="'/'+$route.params.lang+'/instructors/' + instructor.id"
            v-for="(instructor, index) in language.instructors"
            v-if="instructor.user"
            :key="instructor.id"
          >
            <div
              :class="index != 0 ? '-is-spaced-top': ''"
              class="box is-radiusless -card-vertical"
            >
              <div>
                <!-- changed the img tag fot div  -->
                <div
                  v-if="instructor.user.profile_picture"
                  :style="'background-image: url(' + instructor.user.profile_picture + '); background-size: cover; background-repeat: no-repeat'"
                  class="-is-circle -profile-picture"
                />
                <img
                  v-else
                  style="opacity: .2;"
                  src="/profile.png"
                  class="-is-circle -profile-picture"
                >
                <!-- <div v-else class="-profile-picture is-inline-block" /> -->
                <div class="is-inline-block -description">
                  <h5 class="title is-6">
                    {{ instructor.user.name + ' ' + instructor.user.lastname[0] + '.' }}
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
                      {{ instructor.description = truncString(instructor.description,10,'...') }}
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
import Search from '~/components/web/general/Search.vue'
import Rating from '~/components/web/general/Rating.vue'
import axios from 'axios'
export default {
  components: {
    Search,
    Rating
  },
  watchQuery: ['days', 'price'],
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
  created() {
    // eslint-disable-next-line no-console
    console.log(this.lang.instructors)
  },
  methods: {
    truncString(str, max, add) {
      add = add || '...'
      return typeof str === 'string' && str.length > max
        ? str.substring(0, max) + add
        : str
    }
  }
}
</script>
