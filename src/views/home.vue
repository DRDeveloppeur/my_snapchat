<template>
  <div v-if="token" class="home">
    <img alt="Vue logo" src="../assets/snap2.png" width="15%">
    <div class="container">
      <div class="input-group" v-if="image">
        <input type="number" class="form-control"
          v-model="duration">
        <div class="input-group-append">
          <span class="input-group-text">Sec</span>
        </div>
      </div>

      <select v-if="users && image &&!to" class="form-control" v-model="to">
        <hr>
        <option class="custom-select" style="padding-left: -10px !important" v-for="user in users" :key="user.id" >
          {{ user.email }}
        </option>
      </select>
      <p v-if="to" @click="to = ''">{{ to }}</p>

      <div class="input-group">
        <div class="custom-file">
          <input type="file" class="custom-file-input"
          @click="find" id="image" ref="myFiles" @change="file">
          <label class="custom-file-label" for="image">Choose file</label>
        </div>
        <div class="input-group-append">
          <button v-if="image" @click="send"
            class="btn btn-outline-secondary" type="button">
            Button
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'home',
  data () {
    return {
      token: localStorage.token,
      image: '',
      to: '',
      duration: 5,
      users: []
    }
  },
  methods: {
    file (event) {
      this.image = event.target.files[0]
    },
    find () {
      axios.get('https://api.snapchat.wac.epitech.eu/all', {
        headers: {
          token: this.token
        }
      }).then(res => {
        this.users = res.data.data
      })
    },
    send () {
      var formData = new FormData()
      formData.append('duration', this.duration)
      formData.append('to', this.to)
      formData.append('image', this.image)

      axios.post('https://api.snapchat.wac.epitech.eu/snap', formData, {
        headers: {
          'Content-Type': 'multipart/form-data',
          token: this.token
        }
      }).then(res => {
        window.alert('Snap sended')
        window.location.href = '/all'
      })
    }
  }
}
</script>

<style media="screen">
  body {
    word-wrap: break-word;
  }
</style>
