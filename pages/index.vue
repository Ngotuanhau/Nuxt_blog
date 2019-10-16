<template>
  <v-layout column justify-center align-center>
    <TopPost class="mb-10" />
    <v-flex xs12 sm8 md6>
      <Categories />
    </v-flex>
  </v-layout>
</template>

<script>
import TopPost from "~/components/TopPost";
import Categories from "~/components/Categories";

export default {
  components: {
    TopPost,
    Categories
  }
};
</script>