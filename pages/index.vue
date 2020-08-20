<template>
  <div>
    <!-- <nuxt-link
      to="/prueba"
      class="navbar-item"
    >
      prueba
    </nuxt-link> -->
    <!-- Jumbotron -->
    <div class="hero is-medium -is-relative -home-jumbotron">
      <div class="is-overlay" />
      <div class="hero-body has-text-centered">
        <h1 class="title is-3 has-text-white">
          Find a language teacher in just one minute
        </h1>
        <div class="is-inline-block">
          <h4 class="subtitle is-4 has-text-white">
            Which language do you want to learn?
          </h4>
          <search />
        </div>
      </div>
    </div>
    <!-- ./ Jumbotron -->

    <!-- NEW PART -->
    <div class="section">
      <div class="container">
        <h3 class="title title25"> 
          HOW IT WORKS
        </h3>
      </div>
      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <p class="title25 is-4">FIND</p>
              <p>Search for the language you want to learn and choose a teacher who suits you best.</p>
            </div>
            <div class="column">
              <figure class="image">
                <img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png">
              </figure>
            </div>
          </div>
        </div>
      </a>

      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <figure class="image">
                <img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png">
              </figure>
            </div>
            <div class="column">
              <p class="title25 is-4">Book</p>
              <p>Check the teacher‘s availability and book your one-on-one language class right away.</p>
            </div>
          </div>
        </div>
      </a>

      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <p class="title25 is-4">START</p>
              <p>Join your teacher in your one-on-one video class from wherever you feel comfortable. Start unboxing your skillzz...</p>
            </div>
            <div class="column">
              <figure class="image">
                <img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png">
              </figure>
            </div>
          </div>
        </div>
      </a>
    </div>

    <!-- COMMUNITY -->
    <div class="section">
      <div class="container">
        <h3 class="title title25"> 
          JOIN OUR COMMUNITY
        </h3>
      </div>
      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <p class="title25 is-4">STUDENT</p>
              <ul>
                <li>Be flexible: Book classes whenever you have time.</li>
                <li>Profit the most: Join a one-on-one class for a reasonable price.</li>
                <li>No rush to your class: Just start your device and join the class wherever you are.</li>
              </ul>
            </div>
            <div class="column">
              <figure class="image">
                <img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png">
              </figure>
            </div>
          </div>
        </div>
      </a>

      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <figure class="image">
                <img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png">
              </figure>
            </div>
            <div class="column">
              <p class="title25 is-4">TEACHER</p>
              <ul>
                <li>Earn money flexibly: Teach online from home and on your schedule.</li>
                <li>Motivated learners: Work with motivated students who have picked you as their teacher.</li>
                <li>Be creative: Design your own curriculum and teach the way you want.</li>
              </ul>
            </div>
          </div>
        </div>
      </a>

      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <p class="title25 is-4">DO YOU HAVE A QUESTION?</p>
              <p>Please contact us.</p>
            </div>
            <div class="column">
              <figure class="image">
                <img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png">
              </figure>
            </div>
          </div>
        </div>
      </a>
      <a href="#">
        <div class="container box">
          <div class="columns is-mobile">
            <div class="column">
              <p class="title25 is-4">DO YOU LIKE OUR PLATFORM?</p>
              <p>Tell a friend.</p>
            </div>
            <div class="column" />
          </div>
        </div>
      </a>
    </div>
    <!-- /COMMUNITY -->

    <!-- Description -->
    <div class="section">
      <div class="container">
        <h3 class="title is-3 has-text-centered">
          How it works
        </h3>
        <div class="columns">
          <div class="column">
            <div class="box has-text-centered">
              <b-icon
                pack="fas"
                icon="search"
                size="is-medium"
                custom-class="-has-text-primary"
              />
              <h5 class="title is-4 -is-spaced-top -is-marginless-bottom">
                Find
              </h5>
              <p>
                Search for the language you want to learn and choose your teacher
              </p>
            </div>
          </div>
          <div class="column">
            <div class="box has-text-centered">
              <b-icon
                pack="far"
                icon="calendar-alt"
                size="is-medium"
                custom-class="-has-text-primary"
              />
              <h5 class="title is-4 -is-spaced-top -is-marginless-bottom">
                Book
              </h5>
              <p>
                <!-- Review the calendar of your teacher and book your class right away -->
                Check the teacher's availability and book your class right away
              </p>
            </div>
          </div>
          <div class="column">
            <div class="box has-text-centered">
              <b-icon
                pack="far"
                icon="user-circle"
                size="is-medium"
                custom-class="-has-text-primary"
              />
              <h5 class="title is-4 -is-spaced-top -is-marginless-bottom">
                Start
              </h5>
              <p>
                Join your teacher in a one-on-one video class and start learning
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- ./Description -->

    <!-- Join our community -->
    <div class="hero -has-bg-light">
      <div class="hero-body">
        <div class="container has-text-centered">
          <h3 class="title is-3">
            Join our community
          </h3>
          <div class="columns">
            <div class="column">
              <div class="is-inline sing-up-as-student">
                <h4 class="title is-4 is-marginless">
                  Sign up as a student
                </h4>
                <p class="-is-spaced-top">
                  Ready to unbox your skillzz?
                </p>
                <nuxt-link
                  to="/auth/signup"
                  class="button subtitle is-4 -is-spaced-top -is-primary-outlined is-medium -btn-apply"
                >
                  Sign up
                </nuxt-link>
              </div>
            </div>
            <div class="column">
              <div class="is-inline sign-up-as-teacher">
                <h4 class="title is-4 is-marginless">
                  Become a teacher
                </h4>
                <p class="-is-spaced-top">
                  Do you want to join as a teacher?
                </p>
                <nuxt-link
                  to="/teach"
                  class="button subtitle is-4 -is-spaced-top -is-primary-outlined is-medium -btn-apply"
                >
                  Apply now
                </nuxt-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- <div class="hero -has-bg-light">
      <div class="hero-body">
        <div class="container has-text-centered">
          <h3 class="title is-3">
            Become a teacher
          </h3>
          <p>
            Do you want to join as a teacher?
          </p>
          <nuxt-link
            to="/teach"
            class="button -is-spaced-top -is-primary-outlined is-medium -btn-apply"
          >
            Apply today
          </nuxt-link>
        </div>
      </div>
    </div> -->
    <!-- ./Join our community -->

    <div class="section">
      <div class="container has-text-centered subtitle is-4">
        <h4 class="subtitle is-4 is-inline">
          Do you have questions?
        </h4>
        <nuxt-link to="/contact" class="-has-text-primary">
          Contact us
        </nuxt-link>
        <br><br>
        <h4 class="subtitle is-4 is-inline">
          Do you like our platform?
        </h4>
        <!-- <nuxt-link to="/tell-a-friend" class="-has-text-primary">
          Tell a friend
        </nuxt-link> -->
        <a
          href="mailto:?subject=Foreign Language Teachers&amp;body=Hi! I think you should checkout Skillzzbox! They connect students with foreign language teachers for live video classes. Here is the link: www.skillzzbox.com"
          title="Share by Email"
          class="-has-text-primary"
        >
          Tell a friend
        </a>
      </div>
    </div>
    </nuxt-link>
  </div>
</template>
<style lang="sass" scoped>
  @import "~/assets/css/_media-queries.sass"
  .title25
    // font-family: 'Calibri'
    font-size: 25px
    font-weight: 600
    

  .-home-jumbotron
    background-image: url('/learning-languages.jpeg')
    background-position: center
    background-repeat: no-repeat
    background-size: cover
    .is-overlay
      background-color: rgba(0, 0, 0, 0.3)
    .hero-body
      z-index: 9
  .-btn-apply
    width: 200px
  .sing-up-as-student
    +tablet
      float: right
      padding-right: 3rem
  .sign-up-as-teacher
    +tablet
      float: left
      padding-left: 3rem
</style>
<script>
import Search from '~/components/web/general/Search.vue'
export default {
  components: {
    Search
  }
}
</script>
