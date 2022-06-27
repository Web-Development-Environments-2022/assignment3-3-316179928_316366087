<template>
  <div class="container">
    <h1 class="title">Search Page</h1>
    <form action="/action_page.php">
      <label for="recipe_to_search">recipe to search:</label>
      <input type="text" id="recipe_to_search" name="recipe_to_search"><br><br>
      <br>
      <label for="numberOfRecipes">Choose how many recipes:</label>
      <select name="numberOfRecipes" id="numberOfRecipes">
        <option value="5">5</option>
        <option value="10">10</option>
        <option value="15">15</option>
      </select>
      <br>
      <label for="cuisine">Choose cuisine:</label>
      
      <br>
      
      <label for="diet">Choose diet:</label>
      <select name="diet" id="diet">
        <option value="5">5</option>
      </select>
      <br>
      <label for="intolerances">Choose intolerances:</label>
      <select name="intolerances" id="intolerances">
        <option value="5">5</option>
      </select>
    </form>
  </div>
</template>

<script>
//// cuisineVal:
//"African", "American", "British", "Cajun", "Caribbean", "Chinese", "Eastern European", "European", "French", "German", "Greek", "Indian", "Irish", "Italian", "Japanese", "Jewish", "Korean", "Latin American", "Mediterranean", "Mexican", "Middle Eastern", "Nordic", "Southern", "Spanish", "Thai", "Vietnamese"      
export default {
  data() {
    return {
      recipe: null,
      
    };
  },
  
  
};
</script>


<style scoped>

</style>
