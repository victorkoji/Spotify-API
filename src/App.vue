<template>
  <v-app>
    <Header :user="user" />
    <v-main>
      <Spotify titulo="Spotify API" :user="user" />
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
    Footer,
  },
  data: () => {
    return {
      token: "",
      user: {},
    };
  },
  methods: {
    getHashParams() {
      var hashParams = {};
      var e,
        r = /([^&;=]+)=?([^&;]*)/g,
        q = window.location.hash.substring(1);
      while ((e = r.exec(q))) {
        hashParams[e[1]] = decodeURIComponent(e[2]);
      }
      return hashParams;
    },

    userLogado() {
      this.token = this.getHashParams().access_token;

      var myHeaders = new Headers({
        Authorization: `Bearer ${this.token}`,
        Accept: "application/json",
        "Content-Type": "application/json",
      });

      fetch(`https://api.spotify.com/v1/me`, {
        method: "GET",
        dataType: "Json",
        headers: myHeaders,
        credentials: "same-origin",
      })
        .then((response) => {
          return response.json();
        })
        .then((response) => {
          if (response.error) this.user = null;
          else this.user = response;
        })
        .catch((response) => {
          console.log(response);
        });
    },
  },
  beforeMount() {
    this.userLogado();
  },
};
</script>
