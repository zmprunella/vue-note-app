<template>
  <div class="home">
    <h2>Home</h2>
    <div v-if="message">{{ message }}</div>
    <NoteComponent />
  </div>
</template>

<script>
import axiosInstance from "../axiosInstance";
import NoteComponent from "@/components/NoteComponent.vue";

export default {
  name: "HomePage",
  data() {
    return {
      message: "",
    };
  },
  computed: {
    isAuthenticated() {
      return !!localStorage.getItem("authToken");
    },
  },

  methods: {
    logout() {
      localStorage.removeItem("authToken");
      this.$router.push("/login");
    },
  },
  components: {
    NoteComponent,
  },

  async mounted() {
    try {
      const token = localStorage.getItem("authToken");
      if (!token) {
        throw new Error("No token found in local storage");
      }

      const config = {
        headers: {
          Authorization: `Bearer ${token}`,
        },
      };

      const response = await axiosInstance.get(
        "http://localhost:3001/home",
        config
      );
      this.message = response.data.message;
    } catch (error) {
      console.error("Failed to fetch data from the protected route:", error);
    }
  },
};
</script>

<style scoped>
.home {
  font-size: 1.8rem;
  color: rgb(0, 0, 0);
}

h1 {
  color: #2c3e50;
}
</style>
