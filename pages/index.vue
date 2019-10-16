<template>
  <v-layout column justify-center align-center>
    <TopPost />
    <v-flex xs12 sm8 md6></v-flex>
  </v-layout>
</template>

<script>
import TopPost from "~/components/TopPost";

export default {
  components: {
    TopPost
  }
};
</script>