<template>
  <v-app dark>
    <v-app-bar></v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>

    <v-footer app>
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
import AppBar from "~/components/Toolbar";
export default {
  components: {
    vAppBar: AppBar
  }
};
</script>
