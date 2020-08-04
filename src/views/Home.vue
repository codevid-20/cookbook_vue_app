<template>
  <div class="home">
    <button v-on:click="indexRecipes()">Get some data from the api</button>
    
    <h1>{{ message }}</h1>
    <h1>{{ name }}</h1>
    <h1>{{ recipes }}</h1>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      name: "brian",
      recipes: []
    };
  },
  created: function() {},
  methods: {
    indexRecipes: function() {
      console.log("why won't you print out!!!");
      console.log('recipes index...');

      

      axios.get('/api/recipes').then(response => {
        console.log(response);
        this.recipes = response.data;
      })
    }
  }
};
</script>
