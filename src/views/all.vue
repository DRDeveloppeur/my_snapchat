<template>
  <div class="all">
    <div class="container">
      <ul class="list-group" v-if="!image">
        <button v-for="snap in mesnap" :key="snap.snap_id"
         @click="show(id = snap.snap_id, snap.duration)"
         type="button" class="list-group-item list-group-item-action">
          {{ snap.from }}
        </button>
      </ul>
      <div v-if="image">
        <img v-bind:src="image" width="100%" @click="image = ''">
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      mesnap: '',
      id: '',
      image: '',
      duration: '',
      token: localStorage.token
    }
  },
  methods: {
    snaps () {
      axios.get('https://api.snapchat.wac.epitech.eu/snaps', {
        headers: {
          token: this.token
        }
      }).then(res => {
        this.mesnap = res.data.data
      })
    },
    show (id, duration) {
      axios.get('https://api.snapchat.wac.epitech.eu/snap/' + id, {
        headers: {
          token: this.token
        }
      }).then((res) => {
        this.image = res.config.url
        var promise = new Promise((resolve) => {
          setTimeout(resolve, duration + '000')
        })
        return promise
      }).then(res => {
        this.image = ''
        return axios.post('https://api.snapchat.wac.epitech.eu/seen', { id: id }, {
          headers: {
            token: this.token
          }
        })
      }).then(() => {
        location.reload()
        return Promise.resolve()
      })
    }
  },
  mounted () {
    this.snaps()
  }
}
</script>

<style lang="css">
</style>
