<template>
  <div class="container">
    <div v-if="recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.name }}</h1>
        <img :src="recipe.image" class="center" />
      </div>
      <div class="recipe-body">
        <div class="wrapper">
          <div class="wrapped">
            <div class="mb-3">
              <div>Ready in {{ recipe.timeToMake }} minutes</div>
              <div>Likes: {{ recipe.popularity }} likes</div>
            </div>
            <div>
            Ingredients: {{ recipe.ingridients}}
            </div>
          </div>
          <div class="wrapped">
            Instructions: {{ recipe.instructions}}
          </div>
        </div>
      </div>
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    </div>
  </div>
</template>

<script>
export default {
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
.wrapper {
  display: flex;
}
.wrapped {
  width: 50%;
}
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
/* .recipe-header{

} */
</style>
