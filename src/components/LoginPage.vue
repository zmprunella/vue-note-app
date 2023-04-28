<template>
  <div class="login">
    <h2>Login</h2>
    <form @submit.prevent="submitLoginForm">
      <div>
        <label for="email">Email:</label>
        <input
          type="email"
          id="email"
          placeholder="Enter your email"
          v-model="email"
          required
        />
      </div>
      <div>
        <label for="password">Password:</label>
        <input
          type="password"
          id="password"
          placeholder="Enter your password"
          v-model="password"
          required
        />
      </div>
      <button type="submit">Login</button>
    </form>
    <button @click="goBack" class="back-button">Back</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "LoginPage",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async submitLoginForm() {
      try {
        const response = await axios.post("http://localhost:3001/login", {
          email: this.email,
          password: this.password,
        });
        const token = response.data.token;
        localStorage.setItem("authToken", token);
        this.$router.push("/home");
      } catch (error) {
        console.error("Login failed:", error);
      }
    },
    goBack() {
      this.$router.go(-1);
    },
  },
};
</script>

<style scoped>
.login {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 80vh;
}

h1 {
  font-size: 2.5rem;
  color: #42b983;
  margin-bottom: 1.5rem;
}

form {
  border: #2c3e50 solid;
  border-radius: 15px;
  padding: 5rem;
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 0.5rem;
}

input {
  margin-bottom: 1rem;
  padding: 0.5rem;
  font-size: 1rem;
}

button {
  font-size: 1rem;
  margin: 1rem;
  padding: 0.5rem 2rem;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #2c3e50;
}

.back-button {
  top: 1rem;
  left: 1rem;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

.back-button:hover {
  background-color: #2c3e50;
}
</style>
