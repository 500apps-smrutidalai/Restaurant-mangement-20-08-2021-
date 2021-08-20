<template>
  <Header />
  <!-- <Add @on_new_add="addTodo"/> -->
  <h2 class="resthed">List of Restaurants</h2>
  <table border="1" class="sthome">
    <!-- <td style="text-align: center">ID</td> -->
    <td style="text-align: center">NAME</td>
    <td style="text-align: center">ADDRESS</td>
    <td style="text-align: center">CONTACT</td>
    <td style="text-align: center">Status</td>

    <tr v-for="item in restaurants" :key="item.id">
      <!-- <td style="text-align: center">{{ item.id }}</td> -->
      <td>{{ item.name }}</td>
      <td>{{ item.address }}</td>
      <td>{{ item.contact }}</td>
      <td style="text-align: center">
        <router-link :to="'/update/' + item.id">Update</router-link>
        <button type="button" v-on:click="deleteRestaurant(item.id)" >Delete</button>

      </td>
    </tr>
  </table>
</template>

<script>
import Header from "./Header.vue";
// import Add from './Add.vue'
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
    //   name: "",
      restaurants: [],
    };
  },
  components: {
    Header,
    //    Add,
  },
  // data(){
  //     return{
  //         restaurants:{}
  //     }
  // },
  // methods: {
  //     addTodo(item) {

  //         this.restaurants=item
  //     }
  // },
  methods:{
      async deleteRestaurant(id)
      {
           
      
      let result = await axios.delete("http://localhost:3000/restaurants/" + id);
      

      if (result.status == 200) 
      {
        console.warn("delete",result)
        this.loadData()
      }
      } , 
    async loadData(){
        let newuser = localStorage.getItem("user-info");
       
        // this.name = JSON.parse(newuser).name;
        
        if (!newuser) 
        {
            console.warn("inside if block",newuser)
        this.$router.push({name:"SignUp"});
        }
                    console.warn("outside if block",newuser)

        let result = await axios.get("http://localhost:3000/restaurants");

        this.restaurants = result.data;
    }


  },

  async mounted() {
        this.loadData()
  },
};
</script>

<style scoped>
.sthome {
  width: 600px;
  height: 200px;
}

.style {
  text-align: center;
}
</style>

