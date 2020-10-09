<template>
  <v-app>

    <Header titulo="Spotify API" />
    <v-main>
        <Home titulo="Spotify API" />
    </v-main>
    <Footer />

  </v-app>
</template>

<script>
import Header from "./components/Header";
import Home from "./components/Home";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Home,
    Header,
    Footer
  },

  data: () => ({
    //
  }),
};
</script>
