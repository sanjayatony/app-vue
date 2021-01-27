<template>
  <div class="home">
    <h1 class="uppercase text-2xl font-bold mb-4">Hello World</h1>
    <p>
      Hi [{{ name }}],
      <a href="#" @click="logout" class="text-purple-500 hover:text-purple-700">logout</a>
      here.
    </p>
  </div>
</template>

<script>
import axios from "axios";

axios.defaults.withCredentials = true;
axios.defaults.baseURL = "http://dash.test";

export default {
  name: "Dashboard",
  data() {
    return {
      name: "",
    };
  },
  mounted() {
    axios.get("/api/user").then((response) => {
      console.log(response);
      this.name = response.data.name;
    });
  },
  methods: {
    logout() {
      axios.post("/logout").then(() => {
        localStorage.removeItem("isLoggedIn");
        this.$router.push({ name: "Login" });
      });
    },
  },
};
</script>
