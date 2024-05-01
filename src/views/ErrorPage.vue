<template>
  <v-app>
  <v-container fluid class="not-found">
    <v-layout justify-center align-center>
      <v-flex xs12>
        <h1 class="display-1">404</h1>
        <h2 class="display-3">Page Not Found</h2>
        <p class="subtitle-1">Sorry, the page you are looking for does not exist.</p>
      </v-flex>
    </v-layout>
    <v-btn color="primary" to="/">Go to Homepage</v-btn>
  </v-container>
  </v-app>
</template>

<script>
export default {
  name: 'NotFound',
};
</script>

<style scoped>
.not-found {
  height: 100vh;
}
</style>
