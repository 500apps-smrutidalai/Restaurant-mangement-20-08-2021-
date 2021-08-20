<template>
  <div class="addpage" align="center">
    <Header />
    <h1>Add Restaurant</h1>
    <input
      type="text"
      v-model="restaurants.name"
      placeholder="Restaurant Name"
    />
    <input type="text" v-model="restaurants.address" placeholder="Address" />
    <input type="text" v-model="restaurants.contact" placeholder="Contact" />
    <button type="button" v-on:click="addRestaurant()">Add</button>

    <!-- <button v-on:click="addRestaurant()">Add</button>
    <button v-on:click="back()">back</button> -->
  </div>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "Add",
  components: {
    Header,
  },
  data() {
    return {
      restaurants: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },

  // methods: {
  //     addRestaurant() {
  //       console.warn(this.restaurants)
  //         // this.$emit("on_new_add",this.restaurants);
  //     },

  methods: {
    async addRestaurant() {
      const result = await axios.post("http://localhost:3000/restaurants", {
        name: this.restaurants.name,
        address: this.restaurants.address,
        contact: this.restaurants.contact,
      });
      if (result.status == 201) {
        this.$router.push({ name: "Home" });
      }
    },
  },
};

// mounted()
// {
//     let newuser=localStorage.getItem('user-info');
//     if (!newuser)
//     {
//         this.$router.push({name:"SignUp"})
//     }
// }
</script>


<style scoped>
.addpage input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1 px solid skyblue;
}
.addpage button {
  width: 320px;
  height: 40px;
  padding-left: 20px;
  margin-bottom: 30px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>

