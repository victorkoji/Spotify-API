<template>
  <v-app>

    <Header titulo="Spotify API" />
    <v-main>
        <Spotify titulo="Spotify API" />
    </v-main>
    <Footer />

  </v-app>
</template>

<script>
import Header from "./components/Header";
import Spotify from "./components/Spotify";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Spotify,
    Header,
    Footer
  },
};
</script>
