<template>
  <div class="signup">
    <img v-if="status" v-bind:src="`https://http.cat/${status}`">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Name:</label> 
        <input type="text" class="form-control" v-model="name">
        <small v-bind:style="`font-size: ${name.length}px`" v-if="name.length <= 20">You have {{ 20 - name.length }} characters remaining</small>
        <small v-if="name.length > 20">Your username is too long, has to be a max of 20 characters</small>
      </div>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email">
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password">
        <small class="text-danger" v-if="password.length < 6">Your password is too short</small>
        <small v-if="password.length > 20">Your password is too long</small>
      </div>
      <div class="form-group">
        <label>Password confirmation:</label>
        <input type="password" class="form-control" v-model="passwordConfirmation">
        <small v-if="password !== passwordConfirmation">Passwords don't match</small>
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<style>
  
</style>


<script>
import axios from "axios";

export default {
  data: function() {
    return {
      name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      errors: [],
      status: ""
    };
  },
  methods: {
    submit: function() {
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation
      };
      axios
        .post("/api/users", params)
        .then(response => {
          this.$router.push("/login");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          console.log(error.response)
          this.status = error.response.status;
        });
    }
  }
};
</script>
