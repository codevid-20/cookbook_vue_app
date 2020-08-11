<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- <h1>{{ recipes }}</h1> -->
    <div class="alert alert-primary" role="alert">
  A simple primary alert—check it out!
</div>
<div class="alert alert-secondary" role="alert">
  A simple secondary alert—check it out!
</div>
<div class="alert alert-success" role="alert">
  A simple success alert—check it out!
</div>
<div class="alert alert-danger" role="alert">
  A simple danger alert—check it out!
</div>
<div class="alert alert-warning" role="alert">
  A simple warning alert—check it out!
</div>
<div class="alert alert-info" role="alert">
  A simple info alert—check it out!
</div>
<div class="alert alert-light" role="alert">
  A simple light alert—check it out!
</div>
<div class="alert alert-dark" role="alert">
  A simple dark alert—check it out!
</div>
    
    <div v-for="recipe in recipes">
      <h3><a v-bind:href="`/recipes/${recipe.id}`">{{ recipe.title }}</a></h3>
      <p>{{ recipe.directions }}</p>
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
      message: "Welcome to the index page!",
      recipes: []
    };
  },
  created: function() {
    this.indexRecipes();
  },
  methods: {
    indexRecipes: function() {
      console.log('in recipes index');
      axios.get('/api/recipes').then(response => {
        console.log(response.data);
        this.recipes = response.data;
      })
    }
  }
};
</script>
