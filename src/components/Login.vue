<template>
  <div class="max-w-md mx-auto mt-16">
    <h1 class="text-center text-3xl font-bold">Admin Page</h1>
    <form class="p-4">
      <div class="rounded-md shadow-sm -space-y-px">
        <input
          type="text"
          v-model="username"
          required
          class="appearance-none relative rounded-none block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10"
          placeholder="Username"
        />
        <input
          type="password"
          v-model="passwd"
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
      </div>
      <div>
        <button
          @click="login"
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
      username: "",
      passwd: "",
    };
  },
  methods: {
    login() {
      axios.get("/sanctum/csrf-cookie").then((response) => {
        console.log(response);
      });
    },
  },
};
</script>
