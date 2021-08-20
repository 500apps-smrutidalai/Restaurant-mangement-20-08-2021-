<template>
  <div class="register" align="center">
    <h2>Sign Up</h2>
    <input type="name" v-model="name" placeholder="Full Name" />
    <input type="email" v-model="email" placeholder="Email address" />
    <input type="password" v-model="password" placeholder="Password" />
    <button v-on:click="signUp">Sign Up</button>
    <p><router-link to="/login">Log In</router-link></p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      // console.warn("signUp",this.name,this.email,this.password)
      let result = await axios.post("http://localhost:3000/user", {
        name: this.name,
        email: this.email,
        password: this.password,
      });

      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    let newuser = localStorage.getItem("user-info");
    if (newuser)
        {
        this.$router.push({ name: "Home" });
        }
  },
};
</script>
<style scoped>
.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1 px solid skyblue;
}
.register button {
  width: 320px;
  height: 40px;
}
</style>
