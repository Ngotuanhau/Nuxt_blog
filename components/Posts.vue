
<template>
  <v-flex lg9>
    <v-card flat>
      <v-container fluid>
        <v-row dense>
          <v-col v-for="item in firstPost" :key="item.id">
            <v-card class="my-4 pa-4 card-first">
              <v-card-title class="card-first__title">
                <span>{{item.name}}</span>
              </v-card-title>
              <v-img
                :src="'http://localhost:1337' + item.image[0].url"
                class="white--text align-end card-first__image"
              ></v-img>
              <v-card-title class="card-first__shortdesc">
                <v-flex d-flex class="card-first__shortdesc--date">
                  <span>{{item.categories[0].name}}</span>
                  <v-spacer></v-spacer>
                  <span>{{item.created_at | moment("from", "now") }}</span>
                </v-flex>
                <span>{{item.short_description}}</span>
              </v-card-title>
            </v-card>
          </v-col>
        </v-row>
        <v-row dense>
          <v-col cols="6" v-for="item in secondPost" :key="item.id">
            <v-card class="my-4 pa-4 card-second">
              <v-img
                :src="'http://localhost:1337' + item.image[0].url"
                class="white--text align-end card-second__image"
              ></v-img>
              <v-card-title class="card-second__name">
                <v-flex d-flex class="card-second__name--date">
                  <span>{{item.categories[0].name}}</span>
                  <v-spacer></v-spacer>
                  <span>{{item.created_at | moment("from", "now") }}</span>
                </v-flex>
                <span>{{item.name}}</span>
              </v-card-title>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-flex>
</template>

<script>
import gql from "graphql-tag";
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
    firstPost(value) {
      console.log("firstPost", value);
    },
    secondPost(value) {
      console.log("secondPost", value);
    }
  },

  apollo: {
    posts: gql`
      query {
        posts(sort: "created_at:desc", start: 4) {
          id
          name
          created_at
          short_description
          categories {
            name
          }
          image {
            url
          }
        }
      }
    `
  },

  computed: {
    firstPost() {
      return this.posts.slice(0, 1);
    },
    secondPost() {
      return this.posts.slice(1);
    }
  }
};
</script>

<style lang="scss" scoped>
.card-first {
  border-radius: 40px;
  cursor: pointer;

  .card-first__title {
    word-break: initial;
    font-size: 20px;
    font-weight: 500;
    word-spacing: 2px;
  }

  .card-first__image {
    border-radius: 40px;
    height: 400px;
    margin: 9px;
  }

  .card-first__shortdesc {
    word-break: initial;
    font-size: 15px;
    color: rgba(0, 0, 0, 0.7);

    .card-first__shortdesc--date {
      word-spacing: 2px;
      font-size: 18px;
      color: red;
      margin-bottom: 5px;
    }
  }
}

.card-second {
  border-radius: 40px;
  cursor: pointer;

  .card-second__image {
    border-radius: 40px;
    height: 250px;
    margin: 9px;
  }

  .card-second__name {
    word-break: initial;
    font-size: 18px;
    font-weight: 500;

    .card-second__name--date {
      color: red;
      word-spacing: 2px;
      font-size: 18px;
      margin-bottom: 9px;
    }
  }
}
</style>