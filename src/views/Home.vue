<template>
  <div class="home">

    
    <h1>{{ message }}</h1>
    <p>Make a new recipe</p>
    
    <p>Title: <input v-model="newRecipeTitle" type="text"></p>
    <p>Ingredients: <input v-model="newRecipeIngredients" type="text"></p>
    <p>Directions: <input v-model="newRecipeDirections" type="text"></p>
    <p>Prep Time: <input v-model="newRecipePrepTime" type="text"></p>
    <p>Image Url: <input v-model="newRecipeImageUrl" type="text"></p>
    
    <button v-on:click="addRecipe()">Add Recipe</button>
    

    <div v-for="recipe in recipes">
      <br>
      <br>
      <br>
      <br>
      <p>Id: {{recipe.id}}</p>
      <p>title: {{ recipe.title }}</p>
      <p>ingredients: {{ recipe.ingredients }}</p>
      <p>image_url: {{ recipe.image_url }}</p>
      <img v-bind:src="recipe.image_url">      
      <button v-on:click="showInfo(recipe)">Show more info</button>
      <hr>
    </div>


    <dialog id="recipe-details">
      <form method="dialog">
        <h1>Recipe info</h1>
        <p>Id: {{currentRecipe.id}}</p>
        <p>Title: <input v-model="currentRecipe.title"></p>
        <p>Chef: <input v-model="currentRecipe.chef"></p>
        <p>Ingredients: <input  v-model="currentRecipe.ingredients"></p>
        <p>Directions: <input  v-model="currentRecipe.directions"></p>
        <p>Prep time: <input  v-model="currentRecipe.prep_time"></p>
        <p>Image URL: <input  v-model="currentRecipe.image_url"></p>
        <button v-on:click="updateRecipe(currentRecipe)">Update</button>
        <button>Close</button>
        <button v-on:click="destroyRecipe(currentRecipe)">Delete recipe</button>
      </form>
    </dialog>
    
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
      recipes: [],
      newRecipeTitle: "",
      newRecipeIngredients: "",
      newRecipeDirections: "",
      newRecipePrepTime: "",
      newRecipeImageUrl: "",
      currentRecipe: {}
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
      console.log(this.newRecipeTitle);

      var params = {
        title: this.newRecipeTitle,
        prep_time: this.newRecipePrepTime,
        directions: this.newRecipeDirections,
        ingredients: this.newRecipeIngredients,
        image_url: this.newRecipeImageUrl
      }

      axios.post('/api/recipes', params).then(response => {
        console.log(response.data);
        this.recipes.push(response.data);
      })
    },
    showInfo: function(recipe) {
      console.log(recipe);
      this.currentRecipe = recipe;
      document.querySelector('#recipe-details').showModal();
    },
    updateRecipe: function(recipe) {
      console.log(recipe);

      var params = {
        title: recipe.title,
        prep_time: recipe.prep_time,
        directions: recipe.directions,
        ingredients: recipe.ingredients,
        image_url: recipe.image_url
      }

      axios.patch('/api/recipes/' + recipe.id, params).then(response => {
        console.log(response.data);
        this.currentRecipe = response.data;
      })
    },
    destroyRecipe: function(recipe) {
      console.log(recipe);
      // delete it in the backend (rails)
      axios.delete('/api/recipes/' + recipe.id).then(response => {
        console.log(response.data);
        // delete in frontend 
        var index = this.recipes.indexOf(recipe);

        this.recipes.splice(index, 1);
        
        console.log(index);
      })

    }
  }
};


// new/create

// get user input
// keep track of it
  // send that user input to rails
  // get the response from rails
  // take that response and show it to the user



</script>
