<template>
  <v-card color="grey lighten-4" flat tile>
    <v-toolbar extended>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title></v-toolbar-title>
      <img src="@/assets/spotify-seeklogo.com.svg" alt="logo" style="height: 40px;">

      <v-spacer></v-spacer>
      <i class="fa fa-github" aria-hidden="true"></i>

      <v-btn color="secondary" elevation="2">
        <a href="http://localhost:8888/login" class="btn-spotify"
          >Login Spotify</a
        >
      </v-btn>
    </v-toolbar>
  </v-card>
</template>

<script>
export default {
  name: "Header",
  props: {
    titulo: String,
  },
};
</script>

<style>
.btn-spotify {
  color: #6bd06b !important;
}
</style>