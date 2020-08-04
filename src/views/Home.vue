<template>
  <div class="home">

    
    <h1>{{ message }}</h1>
    <h1>{{ name }}</h1>

    <div v-for="recipe in recipes">
      <p>title: {{ recipe.title }}</p>
      <p>ingredients: {{ recipe.ingredients }}</p>
      <p>image_url: {{ recipe.image_url }}</p>
      <hr>
    </div>
    
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
  created: function() {
    this.indexRecipes();
    
  },
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
