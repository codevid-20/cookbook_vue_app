<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- <h1>{{ recipes }}</h1> -->

    <input type="text" v-model="searchTerm">
    <!-- <div v-for="recipe in recipes"> -->
    <div v-for="recipe in filterBy(recipes, searchTerm, 'title')">
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
import Vue2Filters from 'vue2-filters'

export default {
  data: function() {
    return {
      message: "Welcome to the index page!",
      recipes: [],
      searchTerm: "a"
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
  },
  mixins: [Vue2Filters.mixin],
};
</script>
