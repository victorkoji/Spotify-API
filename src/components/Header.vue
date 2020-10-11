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
        
        <ButtonLogoutSpotify titulo="Logout"/>
        
      </div>
      <div v-else>
        <ButtonLoginSpotify titulo="Login Spotify" />
      </div>
    </v-toolbar>
  </v-card>
</template>

<script>
import ButtonLoginSpotify from "./ButtonLoginSpotify";
import ButtonLogoutSpotify from "./ButtonLogoutSpotify";

export default {
  name: "Header",
  props: {
    user: Object,
  },
  components: {
    ButtonLoginSpotify,
    ButtonLogoutSpotify
  }
};
</script>

<style>

</style>