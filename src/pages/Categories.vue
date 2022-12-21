<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>Categories</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Name</th>
              <th scope="col">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(category, index) in categories" :key="category.id">
              <th scope="row">{{ index + 1 }}</th>
              <td>{{ category.name }}</td>
              <td>
                <button class="btn btn-primary">Update</button>
                <button class="btn btn-danger">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: "Categories",
  data() {
    return {
      categories: [],
      baseUrl: "https://news-portal-api-production.up.railway.app",
    }
  },
  methods: {
    async fetchCategories() {
      try {
        const response = await axios({
          method: "GET",
          url: `${this.baseUrl}/categories`,
          headers: {
            access_token: localStorage.access_token,
          },
        })

        this.categories = response.data.dataCategory
      } catch (error) {
        console.log(error)
      }
    },
  },

  async created() {
    await this.fetchCategories()
  },
}
</script>
