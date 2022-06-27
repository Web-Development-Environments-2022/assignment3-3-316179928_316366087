<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'main' }">Vue Recipes</router-link>|
      <router-link :to="{ name: 'search' }">Search</router-link>|
      {{ !$root.store.username }}
      <span v-if="!$root.store.username">
        Guest:
        <router-link :to="{ name: 'register' }">Register</router-link>|
        <router-link :to="{ name: 'login' }">Login</router-link>|
      </span>
      <span v-else>
        <label v-b-modal.add-recipe-modal>Add Recipe</label>|
        <b-modal id="add-recipe-modal" title="Add Recipe" ok-only>
          <AddRecipePage/>
        </b-modal>
        <router-link :to="{ name: 'userRecipes', params: { type: createdString } }">My Recipes</router-link>|
        <router-link :to="{ name: 'userRecipes', params: { type: favoriteString } }">Favorite Recipes</router-link>|
        <router-link :to="{ name: 'familyRecipes' }">Family Recipes</router-link>
        {{ $root.store.username }}: <button @click="Logout">Logout</button>|
      </span>
    </div>
    <router-view />
  </div>
</template>

<script>
import AddRecipePage from './pages/AddRecipePage.vue';
export default {
  components: { AddRecipePage },
  name: "App",
  data() {
    return {
      createdString: "created",
      favoriteString: "favorite"
    };
  },
  methods: {
    Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
