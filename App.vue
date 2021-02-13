<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">
        <i class="demo-icon icon-th"></i>
      </router-link>
      |
      <router-link to="/completed-tasks">
        <i class="demo-icon icon-calendar-check-o"></i>
      </router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  data () {
    return {
      tasks: []
    }
  },
  created () {
    this.fetchData('http://localhost:5000/all')
  },
  methods: {
    fetchData (url) {
      const t = this
      fetch(url)
        .then(resp => resp.json())
        .then(function (data) { t.tasks = data })
    }
  },
  watch: {
    $route (to, from) {
      this.fetchData(`http://localhost:5000/${to.name}`)
    }
  }
}
</script>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css";
@import 'icons/css/fontello.css';

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
