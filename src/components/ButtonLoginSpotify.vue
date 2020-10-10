<template>
  <v-btn color="secondary" elevation="2">
    <a href="http://localhost:8888/login" class="color-spotify">{{ titulo }}</a>
  </v-btn>
</template>

<script>
export default {
  name: "ButtonLoginSpotify",
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