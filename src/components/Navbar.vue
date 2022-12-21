<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">News SPA</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-link" href="#" v-for="nav in navigation">{{ nav }}</a>
        </div>
      </div>
    </div>

    <div class="d-flex">
      <button class="btn btn-outline-success" @click="logout">Logout</button>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    navigation: {
      type: Array,
      required: true,
    },
  },

  methods: {
    logout() {
      localStorage.clear()
    },
  },
}
</script>

<style scoped></style>
