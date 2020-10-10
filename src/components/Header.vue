<template>
  <v-card color="grey lighten-4" flat tile>
    <v-toolbar>
      <!-- <v-app-bar-nav-icon></v-app-bar-nav-icon> -->

      <a href="https://open.spotify.com/" target="_blank">
        <img
          src="@/assets/spotify-seeklogo.com.svg"
          alt="logo"
          style="height: 40px"
        />
      </a>

      <v-spacer></v-spacer>
      <i class="fa fa-github" aria-hidden="true"></i>

      <div v-if="user">
        <v-toolbar-title class="color-spotify">{{ user.display_name }}</v-toolbar-title>
      </div>
      <div v-else>
        <v-btn color="secondary" elevation="2">
          <a href="http://localhost:8888/login" class="color-spotify"
            >Login Spotify</a
          >
        </v-btn>
      </div>
    </v-toolbar>
  </v-card>
</template>

<script>
export default {
  name: "Header",
  props: {
    user: Object,
  },
};
</script>

<style>
.color-spotify {
  color: #6bd06b !important;
}
</style>