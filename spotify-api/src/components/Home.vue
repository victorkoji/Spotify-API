<template>
<div>
    <h1>{{ msg }}</h1>
    <a href="http://localhost:8888" class="btn btn-primary">Log in with Spotify</a>
</div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  },
  methods: {
      getHashParams() {
        var hashParams = {};
        var e, r = /([^&;=]+)=?([^&;]*)/g,
            q = window.location.hash.substring(1);
        while ( e = r.exec(q)) {
            hashParams[e[1]] = decodeURIComponent(e[2]);
        }
        return hashParams;
      }
    }
}
</script>

<style>

</style>