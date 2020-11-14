<template>
 <UserProfile/>
  
</template>

<script>
import UserProfile from "./components/UserProfile"



export default {
  name: 'App',
  components:{
    UserProfile

  }
 
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
    display: flex;
    margin: 0;
    flex-direction: column;
    text-align: center;
  color: #2c3e50;
 
}
</style>
