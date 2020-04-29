<template>
  <div class="columns is-centered mybg">
    <div class="column is-10">
      <b-message type="is-info">
        Select the days and times that you will be available to teach
      </b-message>
      <card :lineBottom="false" title="Schedule">
        <template v-slot:body>
          <h1 style="color:red">
            option 1
          </h1>
          <table class="table is-fullwidth is-striped">
            <thead>
              <tr>
                <th>Day</th>
                <th>Actions</th>
                <th>Start time</th>
                <th>End time</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="day in days" :key="day.day">
                <td>{{ day.name }}</td>
                <td>
                  <button
                    v-if="day.enabled"
                    @click.prevent="disableDay(day)"
                    class="button is-primary -enable  -is-fullwidth"
                  >
                    Enable
                  </button>
                  <button
                    v-else
                    @click.prevent="enableDay(day)"
                    class="button is-danger -disable is-block -is-fullwidth"
                  >
                    Disable
                  </button>
                </td>
                <td>
                  <!-- <b-timepicker
                    v-if="day.enabled"              
                    v-model="day.start_at"
                    :increment-minutes="60"
                    :max-time="maxTime()"
                    size="is-small"  
                    inline              
                  /> -->
                  <b-timepicker                                       
                    v-model="day.start_at"
                    :increment-minutes="60"
                    :max-time="maxTime()"
                    :disabled="!day.enabled" 
                    size="is-small" 
                    inline              
                  />                  
                </td>
                <td>
                  <b-timepicker    
                    v-if="day.enabled"                
                    v-model="day.end_at"
                    :increment-minutes="60"
                    :min-time="minTime(day.start_at)"
                    size="is-small"                
                    inline
                  />
                  <b-timepicker      
                    v-else              
                    v-model="day.end_at"
                    :increment-minutes="60"
                    :min-time="minTime(day.start_at)"
                    size="is-small"
                    disabled
                    inline
                  />
                </td>
              </tr>
            </tbody>
          </table>
          
          <h1 style="color:red">
            option 2
          </h1>
          <table class="table is-fullwidth is-striped">
            <thead>
              <tr>
                <th>Day</th>
                <th>Actions</th>
                <th>Start time</th>
                <th>End time</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="day in days" :key="day.day">
                <td>{{ day.name }}</td>
                <td>
                  <button
                    v-if="day.enabled"
                    @click.prevent="disableDay(day)"
                    class="button is-primary -enable  -is-fullwidth"
                  >
                    Enable
                  </button>
                  <button
                    v-else
                    @click.prevent="enableDay(day)"
                    class="button is-danger -disable is-block -is-fullwidth"
                  >
                    Disable
                  </button>
                </td>
                <td>
                  <b-timepicker
                    v-if="day.enabled"
                    v-model="day.start_at"
                    :increment-minutes="60"
                    :max-time="maxTime()"
                    size="is-small" 
                    inline              
                  />
                </td>
                <td>
                  <b-timepicker
                    v-if="day.enabled"
                    v-model="day.end_at"
                    :increment-minutes="60"
                    :min-time="minTime(day.start_at)"
                    size="is-small"
                    inline
                  />
                </td>
              </tr>
            </tbody>
          </table>
          <h1 style="color:red">
            option 3
          </h1>
          <table class="table is-fullwidth is-striped">
            <thead>
              <tr>
                <th>Day</th>
                <th>Start time</th>
                <th>End time</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="day in days" :key="day.day">
                <td class="size">
                  {{ day.name }}
                </td>
                <td>
                  <b-timepicker
                    v-model="day.start_at"
                    :increment-minutes="60"
                    :max-time="maxTime()"
                    :disabled="!day.enabled"
                    size="is-small"
                    inline
                  />
                </td>
                <td>
                  <b-timepicker
                    v-model="day.end_at"
                    :increment-minutes="60"
                    :min-time="minTime(day.start_at)"
                    :disabled="!day.enabled"
                    size="is-small"
                    inline
                  />
                </td>
                <td>
                  <button
                    v-if="day.enabled"
                    @click.prevent="disableDay(day)"
                    class="button is-primary -enable  -is-fullwidth"
                  >
                    Enable
                  </button>
                  <button
                    v-else
                    @click.prevent="enableDay(day)"
                    class="button is-danger -disable is-block -is-fullwidth"
                  >
                    Disable
                  </button>
                  <!-- <button
                    v-if="day.enabled"
                    @click.prevent="disableDay(day)"
                    class="button is-danger -disable -is-fullwidth"
                  >
                    Disable
                  </button>
                  <button
                    v-else
                    @click.prevent="enableDay(day)"
                    class="button is-primary -enable is-block -is-fullwidth"
                  >
                    Enable
                  </button> -->
                </td>
              </tr>
            </tbody>
            <tfoot>
              <tr>
                <td />
                <td />
                <td />
                <td>
                  <button
                    @click.prevent="updateSchedule"
                    :class="{'is-loading': loading}"
                    class="button -has-bg-primary has-text-white -is-fullwidth"
                  >
                    &nbsp; Save &nbsp;
                  </button>
                </td>
              </tr>
            </tfoot>
          </table>
        </template>
      </card>

      <disable-dates />
    </div>
  </div>
</template>
<script>
import Card from '~/components/general/Card.vue'
import DisableDates from '~/components/panel/instructor/classes/schedule/DisableDates.vue'
import axios from 'axios'
import moment from 'moment'
const midnight = new Date(new Date().setHours(0, 0, 0, 0))
// const midnight = new Date()
// const midnight = '00:00:00'
export default {
  layout: 'panel',
  components: {
    Card,
    DisableDates
  },
  data() {
    return {
      loading: false,
      days: [
        {
          name: 'Monday',
          day: 1,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        },
        {
          name: 'Tuesday',
          day: 2,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        },
        {
          name: 'Wednesday',
          day: 3,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        },
        {
          name: 'Thursday',
          day: 4,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        },
        {
          name: 'Friday',
          day: 5,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        },
        {
          name: 'Saturday',
          day: 6,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        },
        {
          name: 'Sunday',
          day: 0,
          start_at: midnight,
          end_at: midnight,
          enabled: false
        }
      ],
      schedules: []
    }
  },
  mounted() {
    this.getInstructorSchedules()
  },
  methods: {
    test() {
      /* alert('dewdw') */
      return new Date()
    },
    getInstructorSchedules() {
      const user = this.$store.getters['auth/loggedUser']
      const authorization = this.$store.getters['auth/headerAuthorization']
      const url = process.env.apiUrl + 'instructors/' + user.id + '/schedules'

      axios
        .get(url, {
          headers: {
            Authorization: 'Bearer ' + authorization
          }
        })
        .then(response => {
          // this.schedules = response.data
          const schedules = response.data
          this.mergeDays(schedules)
        })
    },
    enableDay(day) {
      day.enabled = true
    },
    disableDay(day) {
      day.enabled = false
    },
    updateSchedule() {
      const user = this.$store.getters['auth/loggedUser']
      const authorization = this.$store.getters['auth/headerAuthorization']
      const url = process.env.apiUrl + 'instructors/' + user.id + '/schedules'
      const data = this.prepareSchedules()
      this.loading = true
      axios
        .post(url, data, {
          headers: {
            Authorization: 'Bearer ' + authorization
          }
        })
        .then(response => {
          this.loading = false
          this.success()
        })
        .catch(() => {
          alert('We had an error updating yuour data')
          this.loading = false
        })
    },
    mergeDays(schedules) {
      const days = this.days
      days.forEach(day => {
        schedules.forEach(schedule => {
          if (day.day === schedule.day) {
            day.enabled = true
            // day.start_at = new Date(schedule.start_at) // creates a Date Object using the clients current time
            day.end_at = new Date(schedule.end_at) // creates a Date Object using the clients current time
            day.start_at = this.parseDateToUserTimezone(schedule.start_at)
            day.end_at = this.parseDateToUserTimezone(schedule.end_at)
          }
        })
      })
    },
    // we use the user timezone saved in our database
    parseDateToUserTimezone(UTCDate) {
      // Difference in minutes betweenn UTCa and user timezone saved in our database
      const offsetMinutesTimezone = this.$store.state.auth.auth.user
        .offset_minutes_timezone
      const date = new Date()
      // Difference in minutes between UTC and user browser timezone
      const browserOffset = date.getTimezoneOffset()
      // read more about returned value with gettimeoffset on https://www.w3schools.com/jsref/jsref_gettimezoneoffset.asp
      const totalOffset = offsetMinutesTimezone + browserOffset
      const newDate = moment(UTCDate).utc()
      totalOffset > 0
        ? newDate.add(totalOffset, 'minutes')
        : newDate.subtract(totalOffset, 'minutes')

      return newDate.toDate()
    },
    prepareSchedules() {
      const schedules = []
      const days = this.days

      days.forEach(day => {
        if (day.enabled) {
          const newDay = {}

          const name = day.name
          delete day.name

          // We store tue time in user timezone to handle user's timezone changes
          newDay.start_at = day.start_at.toString().substring(16, 25)
          newDay.end_at = day.end_at.toString().substring(16, 25)

          // We use toISOString to send date in UTC timezone
          /* newDay.start_at = day.start_at.toISOString().substring(11, 23)
          newDay.end_at = day.end_at.toISOString().substring(11, 23)  */

          newDay.day = day.day

          // schedules.push(day)
          schedules.push(newDay)
          day.name = name
        }
      })
      return schedules
    },
    success() {
      this.$snackbar.open({
        message: `Schedule was updated succesfully`,
        position: 'is-top-right'
      })
    },
    minTime(date) {
      const hour = date.getHours()
      const min = hour + 1
      // create new date to handle two way data binding problems
      const newDate = new Date(date)
      newDate.setHours(min)
      return newDate
    },
    maxTime() {
      const max = new Date()
      max.setHours(22)
      return max
    }
  }
}
</script>
<style scoped>
td {
  vertical-align: middle;
}
.timepicker.dropdown.dropdown-menu.dropdown-content
  div[class='dropdown-item']
  .field
  span[class='control'] {
  display: none;
}
/* .timepicker {
  display: none;
} */
</style>
