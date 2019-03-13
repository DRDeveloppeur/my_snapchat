<template>
  <div id="app">
    <div id="nav">
      <div v-if="token">
        <ul class="display">
          <li class="item">
            <router-link to="/home">Home</router-link> |
          </li>
          <li class="item">
            <router-link to="/all">All</router-link> |
          </li>
          <li class="item">
            <router-link to="/connection"><a @click="logout">Logout</a></router-link>
          </li>
        </ul>
      </div>
      <div v-else>
        <ul class="display">
          <li class="item">
            <router-link class="item" to="/connection">Connection</router-link> |
          </li>
          <li class="item">
            <router-link class="item" to="/inscription">Inscription</router-link>
          </li>
        </ul>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  data () {
    return {
      token: localStorage.getItem('token')
    }
  },
  methods: {
    logout () {
      localStorage.clear()
      window.location.href = '/connection'
    }
  }
}
</script>

<style>
input {
  background-color: black;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

li {
  list-style-type: none;
}

.item a {
  text-decoration: none;
}
.item a:hover {
  color: #4a77d4 !important;
}

ul {
  justify-content: center;
}

.item {
  padding: .15%;
}

.item:hover {
  color: #4a77d4 !important;
}

.item::after {
  content: '';
  display: block;
  width: 0;
  height: 2px;
  background: #4a77d4;
  transition: 0.4s;
}

.display {
  display: flex;
}

.item:hover::after {
  width: 100%;
}

</style>
