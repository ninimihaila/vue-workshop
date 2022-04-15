<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-btn to="/" plain>Home</v-btn>
      <v-btn to="/about" plain>About</v-btn>
      <v-btn to="/weather" plain>Weather</v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
