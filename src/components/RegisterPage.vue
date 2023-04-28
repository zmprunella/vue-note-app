<template>
  <div class="register">
    <h2>Register</h2>
    <form @submit.prevent="submitRegisterForm">
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
      <button type="submit">Register</button>
    </form>
    <button @click="goBack" class="back-button">Back</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "RegisterPage",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async submitRegisterForm() {
      try {
        await axios.post("http://localhost:3001/register", {
          email: this.email,
          password: this.password,
        });
        this.$router.push("/login");
      } catch (error) {
        console.error("Registration failed:", error);
      }
    },
    goBack() {
      this.$router.go(-1);
    },
  },
};
</script>

<style scoped>
.register {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 80vh;
}

h1 {
  font-size: 2.5rem;
  color: #2c3e50;
  margin-bottom: 1.5rem;
}

form {
  display: flex;
  flex-direction: column;
  border-radius: 15px;
  padding: 5rem;
  border: #2c3e50 solid;
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
  padding: 0.5rem 1rem;
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
