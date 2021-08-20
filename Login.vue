<template>
  <div class="login" align="center">
    <form>
      <h2>Log In</h2>

      <input type="email" v-model="email" placeholder="Email address" />
      <input type="password" v-model="password" placeholder="Password" />
      <button v-on:click="logIn">Log In</button>
      <p><router-link to="/sign-up">Sign Up</router-link></p>
    </form>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async logIn() {
      let result = await axios.get(
        `http://localhost:3000/user?email=${this.email}&password=${this.password}`
      );
      //   console.log("aaa",result)
      if (result.status == 201 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringfy(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    let newuser = localStorage.getItem("user-info");
    if (newuser) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>


<style scoped>
.login input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1 px solid skyblue;
}
.login button {
  width: 320px;
  height: 40px;
}
</style>