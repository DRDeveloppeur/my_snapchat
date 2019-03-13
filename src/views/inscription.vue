<template>
  <div class="inscription">
    <h5>Inscription</h5>
    <img alt="Vue logo" src="../assets/snap2.png" width="15%">
    <div class="container">
      <form>
        <div class="email form-group">
          <label for="email">Choose mail</label>
          <input class="form-control" autocomplete="email" v-model="email" type="email" id="email" placeholder="Email" required>
        </div>
        <div class="password form-group">
          <label for="password">Choose password</label>
          <input class="form-control" autocomplete="current-password" v-model="password" type="password" id="password" placeholder="Password" required>
        </div>
        <div class="button">
          <button type="button" @click="inscription" class="btn btn-sm btn-dark" id="button">Register</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'inscription',
  components: {},
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    inscription () {
      axios.post('https://api.snapchat.wac.epitech.eu/inscription', {
        email: this.email,
        password: this.password
      }).then(function (res) {
        console.log(res)
        window.location.href = '/connection'
      })
    }
  },
  created () {
    if (localStorage.token) {
      window.location.href = '/home'
    }
  }
}
</script>

<style lang="css">
</style>
