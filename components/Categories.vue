<template>
  <v-layout wrap>
    <v-flex v-for="item in categories" :key="item.id" xs12 md4>
      <v-hover v-slot:default="{ hover }">
        <v-card class="card">
          <v-img :src="'http://localhost:1337' + item.image.url" class="card-image">
            <v-expand-transition>
              <v-btn v-if="hover" class="orange darken-4 card-image__btn">
                <span class="card-image__text">{{item.name}}</span>
              </v-btn>
            </v-expand-transition>
          </v-img>
        </v-card>
      </v-hover>
    </v-flex>
  </v-layout>
</template>

<script>
import gql from "graphql-tag";

export default {
  data() {
    return {
      categories: []
    };
  },

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
          image {
            url
          }
        }
      }
    `
  }
};
</script>

<style  lang="scss" scoped>
.card {
  margin: 10px;
  border-radius: 20px;

  .card-image {
    height: 200px;
    cursor: pointer;
    display: flex;
    align-items: center;
    text-align: center;

    .card-image__btn {
      border-radius: 20px;
      transition-timing-function: ease-in;

      .card-image__text {
        color: white;
        letter-spacing: 2px;
        font-size: 15px;
        text-transform: capitalize;
      }
    }
  }
}
</style>