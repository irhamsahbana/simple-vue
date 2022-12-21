<script>
import axios from "axios"
import Card from "../components/Card.vue"

export default {
  name: "Dashboard",
  components: {
    Card,
  },

  data() {
    return {
      baseUrl: "https://news-portal-api-production.up.railway.app",
      countNews: 0,
      countCategories: 0,
    }
  },

  methods: {
    async fetchNews() {
      try {
        const response = await axios({
          method: "GET",
          url: `${this.baseUrl}/news`,
          headers: {
            access_token: localStorage.access_token,
          },
        })

        console.log(response.data)
        this.countNews = response.data.data.length
      } catch (error) {
        console.log(error)
      }
    },

    async fetchCategories() {
      try {
        const response = await axios({
          method: "GET",
          url: `${this.baseUrl}/categories`,
          headers: {
            access_token: localStorage.access_token,
          },
        })

        this.countCategories = response.data.dataCategory.length
      } catch (error) {
        console.log(error)
      }
    },
  },

  async created() {
    await this.fetchNews()
    await this.fetchCategories()
  },
}
</script>

<template>
  <div class="d-flex">
      <Card :title="'Number of News'" :content="countNews" />
      <Card :title="'Number of Categories'" :content="countCategories" />
  </div>
</template>
