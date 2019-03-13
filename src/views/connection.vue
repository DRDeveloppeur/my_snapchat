<template>
  <div class="connection">
    <h5>Connection</h5>
    <img alt="Vue logo" src="../assets/snap2.png" width="15%">
    <div class="container">
      <form>
        <div class="email form-group">
          <label for="email">Your mail</label>
          <input class="form-control" autocomplete="email" v-model="email"
            type="email" id="email" placeholder="Email" required>
        </div>
        <div class="password form-group">
          <label for="password">Your password</label>
          <input class="form-control" autocomplete="current-password"
            v-model="password" type="password" id="password"
            placeholder="Password" required>
        </div>
        <div class="button">
          <button type="button" @click="connection" class="btn btn-sm btn-dark"
            id="button">Login</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'connection',
  components: {},
  data () {
    return {
      token: localStorage.token,
      email: '',
      password: ''
    }
  },
  methods: {
    connection () {
      axios.post('https://api.snapchat.wac.epitech.eu/connection', {
        email: this.email,
        password: this.password
      }).then(function (res) {
        if (res.data.data.token) {
          localStorage.setItem('token', res.data.data.token)
          localStorage.setItem('email', res.data.data.email)
          window.location.href = '/home'
        }
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
