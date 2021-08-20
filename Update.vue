<template>
  <div class="updatepage" align="center">
    <h1>Update Restaurant</h1>
    <input type="text" v-model="restaurants.name" placeholder="Enter Name" />
    <input
      type="text"
      v-model="restaurants.address"
      placeholder="Enter Address"
    />
    <input
      type="text"
      v-model="restaurants.contact"
      placeholder="Enter Contact"
    />
    <button type="button" v-on:click="updateRestaurant">Update</button>
  </div>
  <!-- <button v-on:click="addRestaurant()">Add</button>
    <button v-on:click="back()">back</button> -->
</template>

<script>
import axios from "axios";

export default {
  name: "Update",

  data() {
    return {
      restaurants: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },

  methods: {
    async updateRestaurant() {
      console.warn(this.restaurants);
      const result = await axios.put(
        "http://localhost:3000/restaurants/" + this.$route.params.id,
        {
          name: this.restaurants.name,
          address: this.restaurants.address,
          contact: this.restaurants.contact,
        }
      );

      if (result.status == 200) {
        this.$router.push({ name: "Home" });
      }
    },
  },

  async mounted() {
    let newuser = localStorage.getItem("user-info");

    if (!newuser) {
      this.$router.push({ name: "SignUp" });
    }
    const result = await axios.get(
      "http://localhost:3000/restaurants/" + this.$route.params.id
    );
    this.restaurants = result.data;
  },
};
</script>

<style scoped>
.updatepage input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1 px solid skyblue;
}
.updatepage button {
  width: 320px;
  height: 40px;
  padding-left: 20px;
  margin-bottom: 30px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
</style>


