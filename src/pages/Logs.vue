<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>Logs</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Product Name</th>
              <th scope="col">Description</th>
              <th scope="col">Updated By</th>
              <th scope="col">Created At</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(log, index) in logs" :key="log.id">
              <th scope="row">{{ index + 1 }}</th>
              <td>{{ log.name }}</td>
              <td>{{ log.description }}</td>
              <td>{{ log.updatedBy }}</td>
              <td>{{ log.createdAt }}</td>
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
  name: "Logs",
  data() {
    return {
      logs: [],
      baseUrl: "https://news-portal-api-production.up.railway.app",
    }
  },
  methods: {
    async fetchLogs() {
      try {
        const response = await axios({
          method: "GET",
          url: `${this.baseUrl}/histories`,
          headers: {
            access_token: localStorage.access_token,
          },
        })

        this.logs = response.data.data
      } catch (error) {
        console.log(error)
      }
    },
  },

  async created() {
    await this.fetchLogs()
  },
}
</script>
