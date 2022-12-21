<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>News</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Title</th>
              <th scope="col" width="180px">Image</th>
              <th scope="col">Content</th>
              <th scope="col">Category</th>
              <th scope="col">Author</th>
              <th scope="col">Status</th>
              <th scope="col">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(news, index) in news" :key="news.id">
              <th scope="row">{{ index + 1 }}</th>
              <td>{{ news.title }}</td>
              <td><img :src="news.imgUrl" class="img-fluid" /></td>
              <td>{{ news.content }}</td>
              <td>{{ news.Category.name }}</td>
              <td>{{ news.User.username }}</td>
              <td>
                <select v-model="news.status" class="form-control">
                  <option v-for="status in statuses" :value="status">
                    {{ status }}
                  </option>
                </select>
              </td>
              <td>
                <button class="btn btn-primary">Edit</button>
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
  data() {
    return {
      baseUrl: "https://news-portal-api-production.up.railway.app",
      news: [],
      selectedStatus: "",
      statuses: ["Active", "Inactive", "Archived"],
    }
  },

  methods: {
    async getNews() {
      try {
        const response = await axios.get(`${this.baseUrl}/news`, {
          headers: {
            access_token: `${localStorage.getItem("access_token")}`,
          },
        })

        console.log(response.data)
        this.news = response.data.data
      } catch (error) {
        console.log(error)
      }
    },
  },

  async created() {
    await this.getNews()
  },
}
</script>
