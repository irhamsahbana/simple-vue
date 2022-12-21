<script>
import axios from "axios"

export default {
  name: "LoginRegister",
  data() {
    return {
      baseUrl: "https://news-portal-api-production.up.railway.app",
      email: "",
      password: "",

      emailRegister: "",
      passwordRegister: "",
      name: "",
      phone: "",
      address: "",
      isLogin: true,
    }
  },
  methods: {
    async login() {
      try {
        const response = await axios.post(`${this.baseUrl}/users/login`, {
          email: this.email,
          password: this.password,
        })

        localStorage.setItem("access_token", response.data.access_token)

      } catch (error) {
        console.log(error)
      }
    },
    async register() {
      try {
        const response = await axios.post(`${this.baseUrl}/users/register`, {
          email: this.emailRegister,
          password: this.passwordRegister,
          name: this.name,
          phone: this.phone,
          address: this.address,
        })
        console.log(response.data)
      } catch (error) {
        console.log(error)
      }
    },
  },

}
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <h1>Register</h1>
        <div class="mb-3">
          <label for="name" class="form-label">Name</label>
          <input
            type="text"
            class="form-control"
            id="name"
            v-model="name"
            aria-describedby="emailHelp"
          />
        </div>
        <div class="mb-3">
          <label for="email-register" class="form-label">Email address</label>
          <input
            type="email"
            class="form-control"
            id="email-register"
            v-model="emailRegister"
            aria-describedby="emailHelp"
          />
        </div>
        <div class="mb-3">
          <label for="password-register" class="form-label">Password</label>
          <input
            type="text"
            class="form-control"
            id="password-register"
            v-model="passwordRegister"
          />
        </div>
        <div class="mb-3">
          <label for="phone" class="form-label">Phone Number</label>
          <input type="text" class="form-control" id="phone" v-model="phone" />
        </div>
        <div class="mb-3">
          <label for="address" class="form-label">Address</label>
          <input
            type="text"
            class="form-control"
            id="address"
            v-model="address"
          />
        </div>
        <button class="btn btn-primary" @click="register">Register</button>
      </div>
      <div class="col-6">
        <h1>Login</h1>
        <div class="mb-3">
          <label for="email" class="form-label">Email address</label>
          <input
            type="email"
            class="form-control"
            id="email"
            v-model="email"
            aria-describedby="emailHelp"
          />
        </div>
        <div class="mb-3">
          <label for="password" class="form-label">Password</label>
          <input
            type="text"
            class="form-control"
            id="password"
            v-model="password"
          />
        </div>

        <button class="btn btn-primary" @click="login">Login</button>
      </div>
    </div>
  </div>
</template>
