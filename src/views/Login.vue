<template>
  <div class="home">
    <h1 class="text-center text-3xl font-bold mb-4">Admin Page</h1>
    <form action="#" method="POST" @submit.prevent="login">
      <div class="rounded-md shadow-sm -space-y-px">
        <input
          type="email"
          v-model="email"
          required
          class="appearance-none relative rounded-none block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10"
          placeholder="Username"
        />
        <input
          type="password"
          v-model="password"
          required
          autocomplete="current-password"
          placeholder="Password"
          class="appearance-none relative rounded-none block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10"
        />
      </div>
      <div class="text-sm py-2">
        <a href="#" class="text-purple-600 hover:text-purple-500">
          Forgot your password?
        </a>
        or back to
        <router-link to="/" class="text-purple-500 hover:text-purple-700">home</router-link>
      </div>
      <div>
        <button
          type="submit"
          class="w-full py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-purple-600 hover:bg-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500"
        >
          Sign in
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

axios.defaults.withCredentials = true;
axios.defaults.baseURL = "http://dash.test";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    login() {
      axios.get("/sanctum/csrf-cookie").then(() => {
        axios
          .post("/login", {
            email: this.email,
            password: this.password,
          })
          .then((response) => {
            console.log(response);
          })
          .catch((error) => {
            console.log(error.response.data);
          });
      });
    },
  },
};
</script>
