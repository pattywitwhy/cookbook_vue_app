<template>
  <div class="recipes-new">
    <h1>New Recipe</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      <div>
        Title: <input v-model="newRecipeTitle">
      </div>
      <div>
        Chef: <input v-model="newRecipeChef">
      </div>
      <div>
        Prep Time: <input v-model="newRecipePrep_time">
      </div>
      <div>
        Ingredients: <input v-model="newRecipeIngredients">
      </div>
      <div>
        Directions: <input v-model="newRecipeDirections">
      </div>
      <div>
        Image URL: <input v-model="newRecipeImage_url">
      </div>

      <input type="submit" value="Create" class="btn btn-secondary">
    </form>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      newRecipeTitle: "",
      newRecipeChef: "",
      newRecipePrep_time: "",
      newRecipeIngredients: "",
      newRecipeDirections: "",
      newRecipeImage_url: "",
      errors: []
    };
  },

  created: function() {},
  methods: {
    submit: function() {
      console.log("Create the Recipe....");
      var params = {
                    title: this.newRecipeTitle,
                    chef: this.newRecipeChef,
                    prep_time: this.newRecipePrep_time,
                    ingredients: this.newRecipeIngredients,
                    directions: this.newRecipeDirections,
                    image_url: this.newRecipeImage_url
                    };
      axios.post("/api/recipes", params)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>R