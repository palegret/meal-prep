<template>
  <span>
    <v-navigation-drawer
      app
      v-model="drawer"
      class="brown lighten-2"
      dark
      disable-resize-watcher
    >
      <v-list>
        <template v-for="(item, index) in items">
          <v-list-item :key="index">
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider :key="`divider-${index}`"></v-divider>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar app color="brown darken-4" dark>
      <v-app-bar-nav-icon
        class="hidden-md-and-up"
        @click="toggleDrawer()"
      ></v-app-bar-nav-icon>
      <v-spacer class="hidden-md-and-up"></v-spacer>
      <router-link to="/">
        <v-toolbar-title to="/">{{ appTitle }}</v-toolbar-title>
      </router-link>
      <v-btn text class="hidden-sm-and-down ml-3" to="/menu">
        Menu
      </v-btn>
      <v-spacer class="hidden-sm-and-down"></v-spacer>
      <div v-if="!isAuthenticated" class="hidden-sm-and-down">
        <v-btn text class="hidden-sm-and-down mr-2" to="/sign-in">
          SIGN IN
        </v-btn>
        <v-btn color="brown lighten-3" class="hidden-sm-and-down" to="/join">
          JOIN
        </v-btn>
      </div>
      <div v-else>
        <v-btn text class="mr-2" to="/profile">
          PROFILE
        </v-btn>
        <v-btn outlined color="white" @click="signOut">
          SIGN OUT
        </v-btn>
      </div>
    </v-app-bar>
  </span>
</template>

<script>
export default {
  name: 'TheNavigation',
  data() {
    return {
      appTitle: 'Meal Prep',
      drawer: false,
      items: [{ title: 'Menu' }, { title: 'Sign In' }, { title: 'Join' }]
    };
  },
  computed: {
    isAuthenticated() {
      return this.$store.getters.isAuthenticated;
    }
  },
  methods: {
    toggleDrawer() {
      this.drawer = !this.drawer;
    },
    signOut() {
      this.$store.dispatch('userSignOut');
    }
  }
};
</script>

<style scoped>
a {
  color: white !important;
  text-decoration: none;
}
</style>
