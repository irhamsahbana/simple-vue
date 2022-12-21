<script>
import Navbar from "./components/Navbar.vue"

// pages
import LoginRegister from "./components/LoginRegister.vue"
import Dashboard from "./pages/Dashboard.vue"
import Categories from "./pages/Categories.vue"
import Logs from "./pages/Logs.vue"
import News from "./pages/News.vue"

export default {
  components: {
    Navbar,

    // pages
    LoginRegister,
    Dashboard,
    News,
    Categories,
    Logs,
  },

  data() {
    return {
      accessToken: localStorage.access_token,
      currentPage: "LoginRegister",
    }
  },
}
</script>

<template>
  <LoginRegister v-if="!accessToken" />

  <template v-if="accessToken">
    <Navbar :navigation="['Dashboard', 'News', 'Category', 'Logs']" />
    <Dashboard />
    <News />
    <Categories />
    <Logs />
  </template>
</template>

<style scoped></style>
