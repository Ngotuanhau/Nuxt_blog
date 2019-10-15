<template>
  <v-app-bar app>
    <v-toolbar-title class="toolbar-logo">
      <span>
        <nuxt-link class="toolbar-logo__text" to="/">Yummy Blog</nuxt-link>
      </span>
    </v-toolbar-title>
    <template v-slot:extension>
      <div class="toolbar-menu">
        <v-tab>
          <span>
            <nuxt-link to="/" class="toolbar-menu__text">trang chủ</nuxt-link>
          </span>
        </v-tab>
        <v-tab
          v-for="item in categories"
          :key="item.id"
          align-with-title
          background-color="transparent"
        >
          <span>
            <nuxt-link
              to="{name:'categories', params:{id:item.id}}"
              class="toolbar-menu__text"
            >{{item.name}}</nuxt-link>
          </span>
        </v-tab>
      </div>
    </template>
  </v-app-bar>
</template>

<script>
import gql from "graphql-tag";

export default {
  watch: {
    categories(value) {
      console.log(value);
    }
  },

  apollo: {
    categories: gql`
      query {
        categories {
          name
        }
      }
    `
  }
};
</script>

<style lang="scss" scoped>
.toolbar-logo {
  width: 100%;
  display: flex;
  justify-content: center;

  .toolbar-logo__text {
    text-decoration: none;
    color: black;
    font-size: 50px;
  }
}

.toolbar-menu {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  .toolbar-menu__text {
    text-decoration: none;
    color: black;
  }
}
</style>
