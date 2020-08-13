<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/test">Test</router-link> |
      <span v-if="isLoggedIn()" <router-link v-if="isLoggedIn()" to="/logout">Logout</router-link> | </span>
      <router-link to="/recipes/new">Recipes New</router-link> |
      <span v-if="!isLoggedIn()"><router-link to="/signup">Signup</router-link> |</span>
      <span v-if="!isLoggedIn()"><router-link to="/login">login</router-link> |</span>
      
    </div>
    <router-view/>
  </div>
</template>

<style>
  #app {
    background-color: url('assets/watercolor.png');
    font-family: Futura;
  }
</style>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    
    getUserId: function() {
      return localStorage.getItem("user_id");
    }
  }
}
</script>