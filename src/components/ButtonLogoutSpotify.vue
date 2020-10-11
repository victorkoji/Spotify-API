<template>
  <v-btn color="secondary" elevation="2">
    <a href="http://localhost:8080" class="color-spotify">{{ titulo }}</a>
  </v-btn>
</template>

<script>
export default {
name: "ButtonLogoutSpotify",
  props: {
    titulo: String,
  },
};

</script>

<style>
.color-spotify {
  color: #6bd06b !important;
}
</style>