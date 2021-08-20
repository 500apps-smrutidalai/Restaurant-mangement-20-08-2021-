<template>
    <div class=nav>
        
        <router-link to='/'>Home </router-link>
        <router-link to='add'>Add Restaurant </router-link>
        <a v-on:click='logout' href="#">Log Out </a>


    </div>
</template>

<script>
export default {
    name:"Header",

    methods:{
        logout()
        {
          localStorage.clear();  
          this.$router.push({name:'SignUp'})
        
        }
    }       
}
</script>
<style scoped>
.nav{
    background: #333;
    overflow: hidden;
}
.nav a{
    float: left;
    color: #ffeeee;
    text-align: center;
    padding:10px 14px;
    text-decoration: none;
    font-size: 16px;
    margin-right: 4px;

}

</style>