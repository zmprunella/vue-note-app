<template>
  <nav v-if="showNav">
    <div v-if="!isAuthenticated">
      <router-link v-if="showRegisterButton" to="/register"
        >Register Page</router-link
      >
      <router-link v-if="showLoginButton" to="/login">Login Page</router-link>
    </div>
    <div v-else>
      <button @click="logout">Logout</button>
    </div>
  </nav>
  <router-view />
</template>

<script>
export default {
  watch: {
    isAuthenticated(newValue) {
      if (newValue) {
        this.$router.push("/home");
      }
    },
  },
  computed: {
    isAuthenticated() {
      return !!localStorage.getItem("authToken");
    },
    showNav() {
      return this.$route.name !== "Landing";
    },
    showLoginButton() {
      return this.$route.name !== "Login";
    },
    showRegisterButton() {
      return this.$route.name !== "Register";
    },
  },
  methods: {
    logout() {
      localStorage.removeItem("authToken");
      this.$router.push("/login");
    },
  },
};
</script>

<style>
body {
  background: linear-gradient(90deg, #75febe, #ab71f5);
  background-repeat: no-repeat;
  background-attachment: fixed;
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #050505;
}

nav {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

nav a,
nav button {
  font-weight: bold;
  color: #ffffff;
  text-decoration: none;
  background-color: #42b983;
  border: none;
  padding: 10px 15px;
  margin: 0 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

nav a:hover,
nav button:hover {
  background-color: #35a56d;
}

/* Active nav button */
nav a.router-link-exact-active {
  background-color: #35a56d;
}
</style>
