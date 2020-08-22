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
    <div class="section">
      <div class="container">
        <p class="centerText newSubTitle">IMPROVE YOUR LANGUAGE SKILLZZ AT EASE<br> BOOK WHENEVER YOU HAVE TIME<br>JOIN ONE-ON-ONE VIDEO CLASSES FOR ANY BUDGET<br>FIND QUALIFIED AND HIGHLY MOTIVATED TEACHERS</p>
      </div>
    </div>

    <!-- NEW PART -->
    <div class="section">
      <div class="container">
        <h3 class="title title25B titleWorks"> 
          HOW IT WORKS
        </h3>
      </div>
      <div class="container box background-gray">
        <a @click.prevent="goSearch">
          <div class="columns is-mobile paddingFind">
            <div class="column has-text-white morePaddingLeft">
              <p class="title25B  ">FIND</p>
              <p class="fontSizeP">Search for the language you want to learn and choose a teacher who suits you best.</p>
            </div>
            <div class="column centerImagen">
              <figure class="image imageContainer positionSmileKids">
                <img class="is-rounded border" src="kids.jpg">
              </figure>
            </div>
          </div>
        </a>
      </div>

      <div class="container box background-gray marginWorks">
        <a @click.prevent="goSearch">
          <div class="columns is-mobile">
            <div class="column centerImagen">
              <figure class="image imageContainer positionCelGirl">
                <img class="is-rounded border" src="smille-girls.jpg">
              </figure>
            </div>
            <div class="column has-text-white">
              <p class="title25B ">Book</p>
              <p class="fontSizeP">Check the teacher‘s availability and book your one-on-one language class right away.</p>
            </div>
          </div>
        </a>
      </div>

      <div class="container box background-gray">
        <a @click.prevent="goSearch">
          <div class="columns is-mobile">
            <div class="column has-text-white">
              <p class="title25B ">START</p>
              <p class="fontSizeP">Join your teacher in your one-on-one video class from wherever you feel comfortable. Start unboxing your skillzz...</p>
            </div>
            <div class="column centerImagen">
              <figure class="image imageContainer positioYellowGirl">
                <img class="is-rounded border" src="girl-with-yellow-sweater.jpg">
              </figure>
            </div>
          </div>
        </a>
      </div>
    </div>

    <!-- COMMUNITY -->
    <div class="section">
      <div class="container">
        <h3 class="title title25B titleCommunity"> 
          JOIN OUR COMMUNITY
        </h3>
      </div>
      <div class="container box background-gray">
        <nuxt-link to="/auth/signup">
          <div class="columns is-mobile">
            <div class="column morePaddingLeft has-text-white">
              <p class="title25B">
                STUDENT
              </p>
              <ul class="fontSizeP bulletPoint">
                <li>Be flexible: Book classes whenever you have time.</li>
                <li>Profit the most: Join a one-on-one class for a reasonable price.</li>
                <li>No rush to your class: Just start your device and join the class wherever you are.</li>
              </ul>
            </div>
            <div class="column centerImagen">
              <figure class="image imageContainer ṕositionCoffeGirl">
                <img class="is-rounded border" src="girld-with-coffe.jpg">
              </figure>
            </div>
          </div>
        </nuxt-link>
      </div>

      <div class="container box background-gray">
        <nuxt-link to="/teach">
          <div class="columns is-mobile">
            <div class="column centerImagen">
              <figure class="image imageContainer positionCoffeMan">
                <img class="is-rounded border" src="boy-with-coffe.jpg">
              </figure>
            </div>
            <div class="column has-text-white">
              <p class="title25B is-4">
                TEACHER
              </p>
              <ul class="fontSizeP bulletPoint">
                <li>Earn money flexibly: Teach online from home and on your schedule.</li>
                <li>Motivated learners: Work with motivated students who have picked you as their teacher.</li>
                <li>Be creative: Design your own curriculum and teach the way you want.</li>
              </ul>
            </div>
          </div>
        </nuxt-link>
      </div>

      <div class="container box background-gray">
        <nuxt-link to="/contact">
          <div class="columns is-mobile">
            <div class="column has-text-white has-text-centered">
              <p class="title25B">
                DO YOU HAVE A QUESTION?
              </p>
              <p class="title25">
                Please contact us.
              </p>
            </div>
            <div class="column">
              <figure class="image imageContainerTabletMan  positionTabletMan">
                <img class="is-rounded border" src="man-with-a-tablet.jpg">
              </figure>
            </div>
          </div>
        </nuxt-link>
      </div>
      <div class="container box background-gray">
        <a 
          href="mailto:?subject=Foreign Language Teachers&amp;body=Hi! I think you should checkout Skillzzbox! They connect students with foreign language teachers for live video classes. Here is the link: www.skillzzbox.com"
          title="Share by Email"
          class="-has-text-primary"
        >
          <div class="columns is-mobile">
            <div class="column has-text-white has-text-centered">
              <p class="title25B">DO YOU LIKE OUR PLATFORM?</p>
              <p class="title25">Tell a friend.</p>
            </div>
            <div class="column" />
          </div>
        </a>
      </div>
    </div>
    <!-- /COMMUNITY -->

    <!-- /NEW-PART-->

    <!-- Description -->
    <!-- <div class="section">
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
              <p> -->
                <!-- Review the calendar of your teacher and book your class right away -->
                <!-- Check the teacher's availability and book your class right away
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
    </div> -->
    <!-- ./Description -->

    <!-- Join our community -->
    <!-- <div class="hero -has-bg-light">
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
    </div> -->
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

    <!-- <div class="section">
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
        </h4> -->
        <!-- <nuxt-link to="/tell-a-friend" class="-has-text-primary">
          Tell a friend
        </nuxt-link> -->
        <!-- <a
          href="mailto:?subject=Foreign Language Teachers&amp;body=Hi! I think you should checkout Skillzzbox! They connect students with foreign language teachers for live video classes. Here is the link: www.skillzzbox.com"
          title="Share by Email"
          class="-has-text-primary"
        >
          Tell a friend
        </a>
      </div>
    </div>
    </nuxt-link> -->
  </div>
</template>
<style lang="sass" scoped>
  @import "~/assets/css/_media-queries.sass"
  .background-gray
    background-color: #82827a8a
  .background-gray:hover
    background-color: #e84660
  .border
    border: 2px solid #e84660
  .bulletPoint
    list-style: square
    margin-left: 20px
  .centerImagen
    margin: auto
  .centerText
    text-align: center
  .fontSizeP
    font-size: 14px
    font-family: Calibri
  .imageContainer, .imageContainerTabletMan
    // position: absolute
    // top: 0
    // z-index: 1
    width: 140px
    height: 140px
    display: block
    margin: auto
    img
      width: 100%
      height: 100%
  .imageContainerTabletMan
    position: absolute
  .morePaddingLeft
    padding-left: 5px
  .newSubTitle
    color: #82827a8a
    font-family: 'Bradley Hand'
    font-size: 18px 
  .title25B
    // font-family: 'Calibri'
    font-size: 18px
    font-weight: 600
    font-family: 'Bradley Hand'
  .title25
    font-size: 14px
    font-family: Calibri
  .titleWorks, .titleCommunity
    color: #82827ae3
    margin-left: 10px
    margin-bottom: 10px
  .positionTabletMan
      top: 61px
      right: 26px
      z-index: 1



  +tablet
    .fontSizeP
      font-size: 22px
    .newSubTitle
      color: #82827a8a
      font-family: 'Bradley Hand'
      font-size: 20px 
    .title25B
      // font-family: 'Calibri'
      font-size: 25px
      font-weight: 600
      font-family: 'Bradley Hand'
    .title25
      font-size: 25px
    .imageContainer
      position: absolute
      top: 0
      z-index: 1
      width: 240px
      height: 240px
      img
        width: 100%
        height: 100%
    .morePaddingLeft
      padding-left: 45px
    .positionSmileKids
      top: -33px
      right: 30px
    .positionCelGirl
      left: 30px
      top: -93px
    .positioYellowGirl
      top: -81px
      right: 30px
    .ṕositionCoffeGirl
      top: -15px
      right: 30px
      width: 280px
      height: 280px
    .positionCoffeMan
      top: -14px
      left: 30px
      width: 300px
      height: 300px
    .positionTabletMan
      top: -30px
      right: 30px
      width: 300px
      height: 300px
    .marginWorks
      margin-top: 70px
      margin-bottom: 70px
    .paddingFind
      padding-top: 10px
      padding-bottom: 10px
    .titleWorks, .titleCommunity
      margin-left: 45px



  +desktop
    .newSubTitle
      color: #82827a8a
      font-family: 'Bradley Hand'
      font-size: 24px
    .positionSmileKids
      top: -33px
      right: 181px
    .positionCelGirl
      left: 132px
      top: -93px
    .positioYellowGirl
      top: -81px
      right: 133px
    .ṕositionCoffeGirl
      top: -15px
      right: 133px
      width: 280px
      height: 280px
    .positionCoffeMan
      top: -14px
      left: 153px
      width: 300px
      height: 300px
    .positionTabletMan
      top: -30px
      right: 180px
      width: 300px
      height: 300px

    

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
  },
  data() {
    return {
      prueba: 'hola'
    }
  },
  methods: {
    goSearch() {
      this.$router.push('/' + '40' + '/instructors?days=0,1,2,3,4,5,6')
    }
  }
}
</script>
