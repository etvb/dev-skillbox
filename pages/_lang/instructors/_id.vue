<template>
  <div class="section">
    <b-modal :active.sync="isCardModalIntroductionVideo" :width="560" scroll="keep">
      <div>
        <iframe
          :src="videoUrl"
          width="560"
          height="315"
          frameborder="0"
          allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
          style="height: 315px"
          allowfullscreen
        />
      </div>
    </b-modal>
    <div class="container">
      <a @click.prevent="goBack" href="#" class="-has-text-primary">Back to results</a>
      <div class="columns is-centered">
        <div class="column is-8">
          <div class="box is-radiusless -card-details-instructor">
            <!-- In case have course picture -->
            <!-- <div v-if="instructor.course.img"> -->
            <div v-if="instructor.course">
              <div class="columns">
                <div class="column is-7 -column-profile -vertical-flex-align -is-borderless-mobile">
                  <div class="-has-margin-auto">
                    <div class="-is-relative -container-profile-picture -is-fullwidth">
                      <div class="-profile-picture is-inline-block -is-absolute" />
                    </div>
                    <h5 class="title is-5 has-text-centered -name -is-spaced-top">
                      Georg B.
                    </h5>
                    <div v-if="instructor.video_url" class="has-text-centered">
                      <button class="button is-small -is-primary-outlined is-rounded">
                        <span>
                          Watch the introduction video
                        </span>
                      </button>
                    </div>
                  </div>
                </div>
                <div class="column is-hidden-mobile">
                  <figure class="image">
                    <img :src="instructor.course.img">
                  </figure>
                </div>
              </div>
              <hr>
            </div>
            <!-- In case only have profile picture -->
            <div v-else>
              <div v-show="instructor.user" class="-is-relative -container-profile-picture -is-fullwidth has-text-centered">
                <div
                  :style="'background-image: url(' + instructor.user.profile_picture + ')'"
                  class="-profile-picture is-inline-block -is-absolute"
                />
                <!-- <img
                  v-if="instructor.user.profile_picture"
                  :src="instructor.user.profile_picture"
                  class="-is-circle -profile-picture -is-absolute"
                > -->
                <hr>
              </div>
              <h5 class="title is-5 has-text-centered -name">
                {{ adaptedName }}
              </h5>
              <div v-if="instructor.video_url" class="has-text-centered">
                <button @click="openVideo" class="button is-small -is-primary-outlined is-rounded">
                  <span>
                    Watch the introduction video
                  </span>
                </button>
              </div>
            </div>

            <div class="-is-spaced-top">
              <b-tag class="is-rounded -top-badge">
                &nbsp; Top &nbsp;
              </b-tag>
              <rating :rating="4" class="is-pulled-right" />
            </div>
            <p class="-is-spaced-top title is-6">
              {{ instructor.description }}
            </p>
            <div
              id="sticky"
              v-if="!isCalendarModalActive"
              class="box is-radiusless -sticky-data -has-bg-primary"
            >
              <h6 class="title is-6 is-inline-block is-marginless has-text-white">
                Price: ${{ instructor.price_by_class }}/45 Minutes
              </h6>
              <button
                @click="activateCalendarModal"
                class="button is-pulled-right -button-book -is-transparent has-text-white"
              >
                Book
              </button>
              <like class="-like" />
            </div>
            <h6 class="title is-6 -is-marginless-bottom">
              About {{ adaptedName }}
            </h6>
            <div>
              {{ instructor.bio }}
            </div>
            <h6 class="title is-6 -is-spaced-top -is-marginless-bottom">
              Native language
            </h6>
            <p>
              {{ instructorLanguage.english }}
            </p>
            <h6 class="title is-6 -is-spaced-top -is-marginless-bottom">
              Languages that {{ adaptedName }} can teach you
            </h6>
            <p v-for="(language, index) in instructorLanguages" :key="index">
              {{ language }}
            </p>
            <h6 class="title is-6 -is-spaced-top -is-marginless-bottom">
              Location
            </h6>
            <p>
              {{ instructor.user.country }}
            </p>
          </div>
          <!-- End box -->
          <b-modal
            :active.sync="isCalendarModalActive"
            class="-has-bg-primary"
          >
            <div class="box is-radiusless -box-schedule">
              <b-message type="is-info">
                All times shown are in your local time.
              </b-message>
              <h5 class="title is-5 has-text-centered">
                <!-- Select date and time -->
                Fill in the required data to book your class
              </h5>
              <div class="columns is-centered">
                <div class="column is-narrow">
                  <b-field
                    :label="languageToTeach.english + ' level'"
                    :message="langLevelMessage"
                    type="is-info"
                    class="-field-level"
                  >
                    <b-select
                      v-model="selectedOptionLevel"
                      @input="changedLangLevel"
                      expanded
                    >
                      <option
                        v-for="option in optionsLevel"
                        :value="option.level"
                        :key="option.id"
                      >
                        {{ option.level }}
                      </option>
                    </b-select>
                  </b-field>
                  <b-field
                    label="Do you have a topic you would like to cover in this lesson? (e.g. grammar, vocabulary, conversation etc.)"
                    class="-field-level"
                  >
                    <b-input
                      v-model="topic"
                      type="textarea"
                      rows="1"
                      placeholder="I want to learn about animals."
                    />
                  </b-field>
                  <div
                    id="calendar-box"
                    class="box is-inline-block is-paddingless -is-shadowless-desktop"
                  >
                    <b-datepicker
                      v-model="date"
                      :unselectable-days-of-week="unselectableDays"
                      :unselectable-dates="unselectableTimes"
                      :min-date="minDate"
                      :max-date="maxDate"
                      @input="changeTimesSchedule(date)"
                      inline
                    />
                  </div>
                </div>
                <div class="column is-narrow">
                  <div class="box is-fullwidth -times">
                    <h4 class="title is-6">
                      Time
                    </h4>
                    <hr>
                    <div
                      v-for="time in times"
                      :key="time"
                      class="field"
                    >
                      <b-radio
                        v-model="radio"
                        :native-value="time"
                      >
                        {{ time }}
                      </b-radio>
                    </div>
                  </div>
                </div>
              </div>
              <hr>
              <div class="columns">
                <div class="column" />
                <div class="column is-narrow">
                  <div class="field is-grouped">
                    <p class="control">
                      <a
                        @click.prevent="book"
                        :class="{'is-loading': loadingBook}"
                        class="button -has-bg-primary has-text-white"
                      >
                        Book
                      </a>
                    </p>
                    <p class="control">
                      <a
                        @click.prevent="cancelBook"
                        class="button"
                      >
                        Cancel
                      </a>
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </b-modal>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="sass">
@import '~/assets/css/_media-queries.sass'
.-box-schedule
  margin: 0 1rem
  .-times
    +tablet
      margin-top: 140px
.-card-details-instructor
  .-column-profile
    border-right: solid 2px whitesmoke
  .-container-profile-picture
    height: 80px
    .-profile-picture
      height: 80px
      width: 80px
      left: 0
      right: 0
      margin: auto
      background: white
      z-index: 9

      background-position: center
      background-repeat: no-repeat
      background-size: cover
    hr
      position: absolute
      width: 100%
      top: 25%
  .-name
    margin-bottom: 0.2rem!important
  .-sticky-data
    // background-color: #343a40
    margin: 1rem -1.25rem
    .-like
      margin-right: 10px
    .-button-book
      top: -5px
    &.sticky /* The sticky class is added to the header with JS when it reaches its scroll position */
      position: fixed
      top: 0
      width: 100%
      margin: 0
      left: 0
      z-index: 99
      .-button-book
        top: 0
</style>
<script>
import Rating from '~/components/web/general/Rating.vue'
import Like from '~/components/general/Like.vue'
import axios from 'axios'
import { mapGetters } from 'vuex'
// import moment from 'moment'
export default {
  components: {
    Rating,
    Like
  },
  data() {
    const today = new Date()
    return {
      isCalendarModalActive: false,
      isCardModalIntroductionVideo: false,
      date: today,
      minDate: new Date(),
      // minDate: new Date(2020, 0),
      // maxDate: new Date(2020, 3),
      // maxDate from below will be used after january
      maxDate: new Date(
        today.getFullYear(),
        today.getMonth(),
        today.getDate() + 60
      ),
      // instructor: {
      //   course: {
      //     img: '/english-course.jpg'
      //   }
      // },
      loadingBook: false,
      instructorLanguage: [],
      instructorTimezone: false,
      instructor: [],
      times: [],
      radio: '',
      schedules: [],
      unselectableTimes: [],
      languageToTeach: '',
      optionsLevel: [
        { level: 'Proficient', id: 1 },
        { level: 'Advanced', id: 2 },
        { level: 'Upper-intermediate', id: 3 },
        { level: 'Intermediate', id: 4 },
        { level: 'Pre-intermediate', id: 5 },
        { level: 'Elementary', id: 6 },
        { level: 'Beginner', id: 7 }
      ],
      selectedOptionLevel: 'Beginner',
      topic: '',
      langLevelMessage: 'You only know a few words of the language, if that.'
    }
  },
  computed: {
    ...mapGetters({
      user: 'auth/loggedUser',
      loggedIn: 'auth/loggedIn'
    }),
    videoUrl() {
      const video = this.instructor.video_url
      let stringVideo = `https://www.youtube.com/embed/`
      if (!video) return stringVideo
      if (video.includes('=')) {
        const split = video.split('=')
        // stringVideo = `https://www.youtube.com/embed/${split[1]}`
        stringVideo += split[1]
      } else if (video.includes('.be')) {
        const split = video.split('/')
        stringVideo += split[split.length - 1]
      }
      return stringVideo
    },
    adaptedName() {
      const name = this.instructor.user.name
      const lastname = this.instructor.user.lastname
      return name + ' ' + lastname[0] + '.'
    },
    // Languages that can teach the instructor
    instructorLanguages() {
      const languages = this.instructor.languages
      const nameLanguages = []
      languages.forEach(language => {
        const nameLanguage = language.english
        // const levelsLanguage = language.pivot.levels
        const levels = language.pivot.levels
        const levelsLanguage = levels.replace('"Begginer",', '')

        // Remove unnecesary characteres
        const cleanedLevels = levelsLanguage.replace(/\[|\]|"/g, '')
        // replce commas with comma and space
        const removedComasLevels = cleanedLevels.split(',').join(', ')
        // Parse data as will be shown
        const parsedData = nameLanguage + ' (' + removedComasLevels + ')'
        nameLanguages.push(parsedData)
        // nameLanguages.push(language.english)
      })
      return nameLanguages
      // return nameLanguages.join(', ')
    },
    unselectableDays() {
      const schedules = this.schedules
      const days = [1, 2, 3, 4, 5, 6, 0]
      const selectableDays = this.selectableDays(schedules)
      const unselectableDays = days.filter(x => !selectableDays.includes(x))
      return unselectableDays
    }
  },
  async asyncData({ params }) {
    const idInstructor = params.id
    const { data } = await axios.get(
      `${process.env.apiUrl}instructor/${idInstructor}`
    )
    return { instructor: data }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
    this.getLanguage()
    this.getTimezone()
    this.getInstructorSchedules()
    this.unselectableDates()
    this.getLanguageToTeach()
  },
  destroyed() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    openVideo() {
      this.isCardModalIntroductionVideo = true
    },
    goBack() {
      this.$router.back()
    },
    setFieldLevelWidth() {
      const fields = document.querySelectorAll('.-field-level')
      const calendarWidth = document.getElementById('calendar-box').offsetWidth
      fields.forEach(field => {
        field.style.maxWidth = calendarWidth + 'px'
      })
    },
    activateCalendarModal() {
      this.isCalendarModalActive = true
      setTimeout(() => {
        this.setFieldLevelWidth()
      }, 100)
    },
    getLanguageToTeach(idLanguage) {
      idLanguage = this.$route.params.lang
      const url = `${process.env.apiUrl}languages/${idLanguage}`

      axios.get(url).then(response => {
        this.languageToTeach = response.data
      })
    },
    handleScroll(event) {
      const elementSticky = document.getElementById('sticky')
      // Get the offset position of the sticky
      const sticky = elementSticky.offsetTop

      if (window.pageYOffset > sticky) {
        elementSticky.classList.add('sticky')
      } else {
        elementSticky.classList.remove('sticky')
      }
    },
    selectableDays(schedules) {
      const days = []
      schedules.forEach(schedule => {
        days.push(schedule.day)
      })
      return days
    },
    unselectableDates() {
      const dates = this.instructor.disabled_dates
      const unselectableDates = []
      dates.forEach(date => {
        const parsedDate = date.date + 'T' + '00:00:00' // For safari compatibility
        unselectableDates.push(new Date(parsedDate))
      })
      this.unselectableTimes = unselectableDates
    },
    getInstructorSchedules() {
      const url = `${process.env.apiUrl}instructors/${
        this.instructor.id
      }/schedules`
      axios.get(url).then(response => {
        const schedules = response.data
        this.schedules = schedules
      })
    },
    changeTimesSchedule(date) {
      const instructor = this.instructor
      this.getInstructorAvailableTimesAtSpecificDate(instructor.id, date)
    },
    getInstructorAvailableTimesAtSpecificDate(instructorId, date) {
      // const weekDay = date.getDay() // Get the weekday as a number (0-6)
      const day = date.getDate() // Get the day as a number (1-31)
      const month = date.getMonth() // Get the month as a number (0-11)
      const year = date.getFullYear() // Get the year as a four digit number (yyyy)

      const fullDate = `${year}-${month + 1}-${day}`
      const data = { date: fullDate }
      const url = `${
        process.env.apiUrl
      }instructor/${instructorId}/available-times`
      axios
        .get(url, {
          params: data
        })
        .then(response => {
          const data = response.data
          // reverse array to start from lowest
          this.changeClassesToUserTimezone(data.reverse())
        })
        .catch(() => {
          alert('Tuvimos un problema para obtener el calendario del instructor')
        })
    },
    changeClassesToUserTimezone(availableTimesUTC) {
      let times = []
      times = availableTimesUTC.map(time => {
        const date = this.parseDateToUserTimezone(time)
        return date
      })
      this.times = times
    },
    parseDateToUserTimezone(UTCDate) {
      // const timezoneInstructor = this.instructor.user.timezone
      let timezone = Intl.DateTimeFormat().resolvedOptions().timeZone
      if (this.loggedIn) timezone = this.user.timezone
      const d = new Date(UTCDate).toLocaleString('en-US', {
        timeZone: timezone,
        hour12: false,
        hour: '2-digit',
        minute: '2-digit'
      })
      // remove 0's at the begin of the time
      const dWithout0AtTheBeginning = d.indexOf('0') === 0 ? d.substring(1) : d
      return dWithout0AtTheBeginning
    },
    book() {
      const time = this.radio
      if (!time.length) return alert('Please select a time')

      this.loadingBook = true
      const date = this.date
      // const parsedDate = date.toJSON().slice(0, 10)
      // const weekDay = date.getDay() // Get the weekday as a number (0-6)
      const day = date.getDate() // Get the day as a number (1-31)
      const month = date.getMonth() // Get the month as a number (0-11)
      const year = date.getFullYear() // Get the year as a four digit number (yyyy)
      const parsedDate = `${year}-${month + 1}-${day}`
      this.$store.commit('cart/addClassToCart', {
        languageLevel: this.selectedOptionLevel,
        time: time,
        topic: this.topic,
        date: parsedDate,
        instructor: this.instructor,
        language: this.$route.params.lang
      })
      this.$router.push('/cart')
    },
    cancelBook() {
      this.isCalendarModalActive = false
    },
    getLanguage() {
      if (this.instructor.user.language_id) {
        const url = `${process.env.apiUrl}languages/${
          this.instructor.user.language_id
        }`
        axios.get(url).then(response => {
          this.instructorLanguage = response.data
        })
      }
    },
    getTimezone() {
      const url = `${process.env.apiUrl}timezones/${
        this.instructor.user.timezone_id
      }`
      axios.get(url).then(response => {
        this.instructorTimezone = response.data
      })
    },
    changedLangLevel() {
      const selectedOptionLevel = this.selectedOptionLevel
      switch (selectedOptionLevel) {
        case 'Proficient':
          this.langLevelMessage =
            "You're fluent, pretty much mother tongue, extremely comfortable, you have complete control over the language."
          break

        case 'Advanced':
          this.langLevelMessage =
            'Comfortable in most situations, strong vocabulary, few errors.'
          break

        case 'Upper-intermediate':
          this.langLevelMessage =
            "You're comfortable in most situations, still some good mistakes."
          break

        case 'Intermediate':
          this.langLevelMessage =
            'Now you can converse in many situations, with less serius errors.'
          break

        case 'Pre-intermediate':
          this.langLevelMessage =
            'Limited vocabulary, but with some help you can participate in basic conversations. You still make a lot of big mistakes.'
          break

        case 'Elementary':
          this.langLevelMessage =
            'You can ask a few basic questions and ideas, but with a lot of mistakes'
          break

        case 'Beginner':
          this.langLevelMessage =
            'You only know a few words of the language, if that'
          break
        default:
          this.langLevelMessage = ''
          break
      }
    }
  }
}
</script>
<style lang="sass">
.-times
  .b-radio
    width: 100%
    .control-label
      margin-left: auto
</style>
