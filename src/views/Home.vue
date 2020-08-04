<template>
  <div class="home">

    
    <h1>{{ message }}</h1>
    <p>Make a new recipe</p>
    <button v-on:click="addRecipe()">Add Recipe</button>
    

    <div v-for="recipe in recipes">
      <p>title: {{ recipe.title }}</p>
      <p>ingredients: {{ recipe.ingredients }}</p>
      <p>image_url: {{ recipe.image_url }}</p>
      <img v-bind:src="recipe.image_url">      
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
    },
    addRecipe: function() {
      console.log('adding recipe...');

      var params = {
        title: "THIS IS A BRAND NEW RECIPE!!!",
        prep_time: 200,
        directions: "here are the directions",
        ingredients: "here are the ingredients",
        image_url: "http://something.com"
      }

      axios.post('/api/recipes', params).then(response => {
        console.log(response.data);
        this.recipes.push(response.data);
      })
    }
  }
};
</script>
