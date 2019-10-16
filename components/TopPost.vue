<template>
  <v-layout row wrap>
    <v-flex v-for="item in topPost" :key="item.id" xs12 md6 lg3>
      <v-hover v-slot:default="{ hover }">
        <v-card class="card">
          <v-img :src="'http://localhost:1337' + item.image[0].url" class="card-image">
            <v-expand-transition>
              <div v-if="hover" class="orange darken-4 v-card--reveal" style="height: 50%;">
                <span class="card-image__time">{{item.created_at | moment("from", "now") }}</span>
                <span class="card-image__text">{{item.name}}</span>
              </div>
            </v-expand-transition>
          </v-img>
        </v-card>
      </v-hover>
    </v-flex>
  </v-layout>
</template>

<script>
import gql from "graphql-tag";
import moment from "vue-moment";

export default {
  data() {
    return {
      posts: []
    };
  },

  watch: {
    posts(value) {
      console.log(value);
    },
    topPost(value) {
      console.log(value);
    }
  },

  apollo: {
    posts: gql`
      query {
        posts(sort: "created_at:desc") {
          name
          created_at
          image {
            url
          }
        }
      }
    `
  },

  computed: {
    topPost() {
      return this.posts.slice(0, 4);
    }
  }
};
</script>

<style lang="scss" scoped>
.card {
  margin: 3px;

  .card-image {
    min-height: 400px;
    max-width: 100%;
    cursor: pointer;

    .v-card--reveal {
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0.7;
      position: absolute;
      bottom: 0;
      width: 100%;

      .card-image__time {
        font-size: 20px;
        color: #fff;
        position: absolute;
        top: 15px;
      }

      .card-image__text {
        font-size: 20px;
        color: #fff;
        padding: 0 20px;
        position: absolute;
        bottom: 10px;
      }
    }
  }
}
</style>