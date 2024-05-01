/* eslint-disable */
<template>
  <div id="app">
    <v-main>
      <v-container fluid>
    <router-view/>
  </v-container>
  <v-footer
    dark
    padless
  >
    <v-card
      class="flex"
      flat
      tile
    >
      <v-card-title class="teal">
        <strong style="font-family: Helvetica;" class="subheading">Created by Poly Mokashi & Sam Gade</strong>

        <v-spacer></v-spacer>

        <v-btn
          v-for="icon in icons"
          :key="icon"
          class="mx-4"
          dark
          icon
        >
          <v-icon size="24px">
            {{ icon }}
          </v-icon>
        </v-btn>
      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>Part Number System</strong>
      </v-card-text>
    </v-card>
  </v-footer>
  </v-main>
  </div>
</template>

<script>
  export default {
    data: () => ({
      icons: [
        'mdi-facebook',
        'mdi-twitter',
        'mdi-linkedin',
        'mdi-instagram',
      ],
    }),
  }
</script>
