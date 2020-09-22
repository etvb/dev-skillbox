<template>
  <div class="hero">
    <div class="hero-body">
      <div class="container">
        <div v-show="$store.state.auth.auth.loggedIn">
          <b-message
            type="is-warning"
            class="-is-spaced"
          >
            Log out before register a new user
          </b-message>
        </div>
        <div
          v-show="!$store.state.auth.auth.loggedIn"
          class="columns is-centered"
        >
          <div class="column is-4">
            <form @submit.prevent="register" action="/register">
              <card title="Sign Up" class="blueColor">
                <template v-slot:body>
                  <b-message
                    v-if="errorsValidation && uncatchedError === false"
                    type="is-danger"
                    class="-is-spaced"
                  >
                    <ul>
                      <li
                        v-for="(error, index) in errorsValidation"
                        :key="index"
                      >
                        {{ error[0] }}
                      </li>
                    </ul>
                  </b-message>
                  <b-message
                    v-if="uncatchedError"
                    type="is-danger"
                    class="-is-spaced"
                  >
                    We have a problem with your register
                  </b-message>
                  <b-field label="First Name">
                    <b-input id="inputName" v-model="name" class="blueColor" required />
                  </b-field>
                  <b-field label="Last Name">
                    <b-input id="inputLastName" class="blueColor" v-model="lastname" required />
                  </b-field>
                  <b-field label="Email">
                    <b-input
                      id="inputEmail"
                      class="blueColor"
                      v-model="email"
                      type="email"
                      required
                    />
                  </b-field>
                  <b-field label="Password">
                    <b-input
                      id="inputPassword"
                      class="blueColor"
                      v-model="password"
                      type="password"
                      required
                    />
                  </b-field>
                  <div class="field">
                    <b-checkbox
                      v-model="acceptGeneralTerms"
                      name="acceptGeneralTerms"
                      type="is-info"
                      required
                    >
                      Accept our
                      <nuxt-link to="/terms-and-conditions" target="_blank" class="has-text-info">
                        general terms
                      </nuxt-link>
                    </b-checkbox>
                  </div>
                  <div class="field">
                    <b-checkbox
                      v-model="acceptPricingTerms"
                      name="acceptPricingTerms"
                      type="is-info"
                      required
                    >
                      Accept our
                      <nuxt-link to="/pricing-terms" target="_blank" class="has-text-info">
                        pricing terms
                      </nuxt-link>
                    </b-checkbox>
                  </div>
                </template>
                <template v-slot:footer-right-actions>
                  <div>
                    <button
                      :class="{'is-loading': loading}"
                      type="submit"
                      class="button -has-bg-primary has-text-white"
                    >
                      Register
                    </button>
                  </div>
                </template>
                <template v-slot:help>
                  <div class="has-text-centered is-size-7">
                    <p class="is-size-7">
                      Do you already have an account?
                    </p>
                    <nuxt-link to="/auth/login">
                      Log In
                    </nuxt-link>
                  </div>
                </template>
              </card>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="sass" scoped>
  hr
    background-color: red
    height: 1px
  .blueColor, 
    border-radius: 4px
    box-shadow: inset 0 1px 2px white
    border: 2px solid #167df0




    

</style>
<script>
import Card from '~/components/general/Card.vue'
import axios from 'axios'
export default {
  components: {
    Card
  },
  data() {
    return {
      loading: false,
      name: '',
      email: '',
      lastname: '',
      password: '',
      acceptGeneralTerms: false,
      acceptPricingTerms: false,
      uncatchedError: false,
      errorsValidation: false
    }
  },
  mounted() {
    this.withoutShadow()
  },
  methods: {
    withoutShadow() {
      const $inputName = document.getElementById('inputName')
      const $inputLastName = document.getElementById('inputLastName')
      const $inputEmail = document.getElementById('inputEmail')
      const $inputPassword = document.getElementById('inputPassword')
      const $hr = document.getElementsByTagName('hr')

      $inputName.style.boxShadow = 'inset 0 1px 2px white'
      $inputName.style.borderColor = 'white'

      $inputLastName.style.boxShadow = 'inset 0 1px 2px white'
      $inputEmail.style.boxShadow = 'inset 0 1px 2px white'
      $inputPassword.style.boxShadow = 'inset 0 1px 2px white'

      $inputLastName.style.borderColor = 'white'
      $inputEmail.style.borderColor = 'white'
      $inputPassword.style.borderColor = 'white'

      $hr[5].style.backgroundColor = '#e84660'
      $hr[6].style.backgroundColor = '#e84660'
    },
    register() {
      this.loading = true
      const url = process.env.apiUrl + 'auth/signup'
      const data = {
        name: this.name,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
        role: 'student',
        timezone: Intl.DateTimeFormat().resolvedOptions().timeZone,
        acceptGeneralTerms: this.acceptGeneralTerms,
        acceptPricingTerms: this.acceptPricingTerms
        // role: document.getElementById('role').value
      }
      axios
        .post(url, data)
        .then(response => {
          // eslint-disable-next-line no-console
          // console.log(response.data)
          this.loading = false
          const user = response.data
          this.$store.commit('auth/logInUser', user.user)
          this.$store.commit('auth/access', {
            access_token: user.access_token,
            expires_at: user.expires_at
          })

          this.success()
          this.goToPanel()
        })
        .catch(error => {
          // eslint-disable-next-line no-console
          // console.log(error.response)
          this.loading = false
          if (error.response.status === 422) {
            this.uncatchedError = false
            this.errorsValidation = error.response.data.errors
            return
          }
          this.errorsValidation = false
          this.uncatchedError = true
        })
    },
    success() {
      this.errorsValidation = false
      this.name = ''
      this.email = ''
      this.password = ''
      this.$snackbar.open({
        duration: 7000,
        message: 'Successfully registered user!',
        type: 'is-success',
        position: 'is-top-right',
        actionText: 'Ok'
      })
    },
    goToPanel() {
      // const loggedAs = this.$store.getters.loggedAs
      window.fbq('track', 'Lead')
      this.$router.push('/panel/student')
      // if (loggedAs == 'instructor') {
      //   this.$router.push('/en/panel/instructor')
      // } else {
      //   this.$router.push('/en/panel/student')
      // }
    }
  }
}
</script>
