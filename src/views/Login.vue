<template>
  <div class="home">
    <h1 class="text-center text-3xl font-bold mb-4">Admin Page</h1>
    <div v-if="blocked" class="text-gray-900 mb-4 text-center">
      <div class="text-red-600 font-bold text-sm">Too much login attempts, please wait.</div>
      <div class="text-gray-900 text-xl font-bold">{{ timerCount }}</div>
    </div>
    <div v-if="errorMessage && !blocked" class="text-red-500 mb-4 text-sm">
      {{ errorMessage }}
    </div>
    <form v-if="!blocked" action="#" method="POST" @submit.prevent="login">
      <div class="rounded-md shadow-sm -space-y-px">
        <input
          type="email"
          v-model="email"
          required
          class="appearance-none relative rounded-none block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10"
          placeholder="Email"
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
        <router-link to="/forgot-password" class="text-purple-600 hover:text-purple-500">
          Forgot your password?
        </router-link>
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
      errorMessage: "",
      counter: 0,
      timerCount: 0,
      blocked: false,
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
          .then(() => {
            localStorage.setItem("isLoggedIn", "true");
            this.$router.push({ name: "Dashboard" });
          })
          .catch((error) => {
            this.counter += 1;
            if (this.counter === 3) {
              this.timerCount = 600;
              this.blocked = true;
            }
            const key = Object.keys(error.response.data.errors)[0];
            this.errorMessage = error.response.data.errors[key][0];
          });
      });
    },
  },
  watch: {
    timerCount: {
      handler(value) {
        if (value > 0) {
          setTimeout(() => {
            this.timerCount--;
          }, 1000);
        }
      },
      immediate: true,
    },
  },
};
</script>
