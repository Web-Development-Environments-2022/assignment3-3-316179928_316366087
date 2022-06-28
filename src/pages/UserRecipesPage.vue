<template>
  <div class="container">
    <RecipePreviewList v-if="paramRecived" :title="userOrFavorite" :prev="previewForUserRecipesPage" label="serach recipe"/>
      <b-button @click="clicked">Button</b-button>

  </div>
</template>

<script>
import RecipePreviewList from '../components/RecipePreviewList.vue';
export default {
  name: "no",
  data() {
    return {
      previewForUserRecipesPage: Object,
      paramRecived: false,
      userOrFavorite: ''
    };
  },
  mounted() {
    this.onPageLoad();
  },
  methods: {
    async onPageLoad() {
      var callType = this.$route.params.type
      const response = await this.axios.get("http://127.0.0.1" + "/recipes/getUserRecipes",
      {
        params: {
          type: callType
        }
      });
      if (callType == "created"){
        this.userOrFavorite = "User Recipes"
      }
      else{
        this.userOrFavorite = "User Favorite Recipes"
      }
      this.previewForUserRecipesPage = response
      this.paramRecived=true
    },
  },
  components: { RecipePreviewList }
};
</script>

<style scoped>
</style>
