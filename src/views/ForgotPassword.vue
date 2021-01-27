<template>
  <div class="home">
    <h1 class="text-center text-3xl font-bold mb-4">Forgot Password</h1>
    <div v-if="errorMessage" class="text-red-500 mb-4 text-sm">
      {{ errorMessage }}
    </div>
    <form action="#" method="POST" @submit.prevent="forgotPassword">
      <div class="rounded-md shadow-sm mb-4">
        <input
          type="email"
          v-model="email"
          required
          class="appearance-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10"
          placeholder="Email"
        />
      </div>
      <div>
        <button
          type="submit"
          class="w-full py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-purple-600 hover:bg-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500"
        >
          Send
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
  name: "ForgotPassword",
  data() {
    return {
      email: "",
      errorMessage: "",
    };
  },
  methods: {
    forgotPassword() {
      //axios.get("/sanctum/csrf-cookie").then(() => {
      axios
        .post("/forgot-password", {
          email: this.email,
        })
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
      //});
    },
  },
};
</script>
