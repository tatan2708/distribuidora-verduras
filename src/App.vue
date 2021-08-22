<template>
  <v-app>
    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  components: {
    
  },
  data: () => ({
    //
  }),
};
</script>

<style lang="scss">
@import "@/scss/variables.scss";

  v-app {
    font-family: $body-font-family !important;
  }

</style>
