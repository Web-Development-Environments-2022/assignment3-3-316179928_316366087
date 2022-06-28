<template>
  <div id="app">
    <b-navbar id="nav" toggleable="md" type="dark" variant="info">
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item :to="{ name: 'main' }">Vue Recipes</b-nav-item>
        <b-nav-item :to="{ name: 'search' }">Search</b-nav-item>
      </b-navbar-nav>
        <b-navbar-nav v-if="!$root.store.username" right>
          <b-nav-text>Guest</b-nav-text>
          <b-nav-item :to="{ name: 'register' }" right>Register</b-nav-item>
          <b-nav-item :to="{ name: 'login' }" right>Login</b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav v-else>
          <b-nav-item v-b-modal.add-recipe-modal>Add Recipe</b-nav-item>
          <b-modal id="add-recipe-modal" title="Add Recipe" ok-only>
            <AddRecipePage/>
          </b-modal>
          <b-nav-item-dropdown text="Personal">
            <b-dropdown-item :to="{ name: 'userRecipes', params: { type: createdString } }">My Recipes</b-dropdown-item>
            <b-dropdown-item :to="{ name: 'userRecipes', params: { type: favoriteString } }">Favorite Recipes</b-dropdown-item>
            <b-dropdown-item :to="{ name: 'familyRecipes' }">Family Recipes</b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-text>{{ $root.store.username }} </b-nav-text>
          <b-nav-item @click="Logout">Logout</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
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

#nav a.b-nav-item-exact-active {
  color: #42b983;
}
</style>
