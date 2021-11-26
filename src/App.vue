<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/register">Register</router-link>|
      <router-link to="/login">Login</router-link>|
      <router-link to="/dashboard">DashBoard</router-link>|
      <button type="submit" @click.prevent="logout">LOG OUT</button>
    </div>
    <router-view/>
  </div>
</template>

<script>
import User from './apis/User'
export default {
  methods: {
    logout() {
      User.logout()
      .then(() => {
        localStorage.removeItem('auth')
        this.$router.push('/')
      })
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
</style>
