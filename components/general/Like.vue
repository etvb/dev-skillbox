<template>
  <a
    @click.prevent="like"
    href="javascript:void(0)"
    class="is-pulled-right"
  >
    <b-icon
      :pack="liked ? 'fas' : 'far'"
      icon="heart"
      class="has-text-black"
      size="is-medium"
    />
  </a>  
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      liked: false
    }
  },
  methods: {
    like() {
      if (this.liked) this.liked = false
      else this.liked = true
      if (!this.isLoggedin) return
      this.storeLike()
    },
    storeLike() {
      const idInstructor = this.$route.params.id
      const user = this.$store.getters['auth/loggedUser']
      const url = `${process.env.apiUrl}instructors/${idInstructor}/like`
      const data = {
        liked: this.liked,
        studentId: user.id
      }
      axios.post(url, data)
      // .then(response => {
      //   // eslint-disable-next-line
      //   console.log(response.data)
      // })
      // .catch(error => {
      //   // eslint-disable-next-line
      //   console.log(error.response)
      // })
    },
    isLoggedin() {
      const loggedIn = this.$store.getters['auth/loggedIn']
      return loggedIn
    }
  }
}
</script>
