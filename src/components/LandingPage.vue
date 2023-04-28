<template>
  <h1>Welcome to the HomePage</h1>
  <div class="landing">
    <div class="buttons-container">
      <router-link to="/login" class="button login">Login</router-link>
      <router-link to="/register" class="button register">Register</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "LandingPage",
};
</script>

<style scoped>
.landing {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
}

.buttons-container {
  display: flex;
  justify-content: space-around;
  width: 50%;
}

.button {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40%;
  height: 5rem;
  font-size: 1.5rem;
  text-decoration: none;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.login {
  background-color: #42b983;
  color: white;
}

.register {
  background-color: #2c3e50;
  color: white;
}

.button:hover {
  background-color: #34495e;
}
</style>
