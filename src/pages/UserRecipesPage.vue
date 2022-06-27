<template>
  <div class="container">
    <RecipePreviewList/>
  </div>
</template>

<script>
import RecipePreviewList from '../components/RecipePreviewList.vue';
export default {
  components: { RecipePreviewList },
  data() {
    return {
      recipe: null
    };
  },
  async created() {
    try {
      let response;
      // response = this.$route.params.response;

      try {
        response = await this.axios.get(
          // "https://test-for-3-2.herokuapp.com/recipes/info",
          // this.$root.store.server_domain + "/recipes/info",
          "http://127.0.0.1:80" + "/recipes/recipe",
          {
            params: { recipeId: this.$route.params.recipeId }
          }
        );

        // console.log("response.status", response.status);
        if (response.status !== 200) this.$router.replace("/NotFound");
      } catch (error) {
        console.log("error.response.status", error.response.status);
        this.$router.replace("/NotFound");
        return;
      }

      let {
            name,
            timeToMake,
            popularity,
            whoCanEatVegOrNot,
            glutenFree,
            wasWatchedByUserBefore,
            wasSavedByUser,
            image,
            ingridients,
            instructions,
            numberOfMeals
      } = response.data;


      let _recipe = {
        name,
        timeToMake,
        popularity,
        whoCanEatVegOrNot,
        glutenFree,
        wasWatchedByUserBefore,
        wasSavedByUser,
        image,
        ingridients,
        instructions,
        numberOfMeals
      };

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style scoped>
</style>
