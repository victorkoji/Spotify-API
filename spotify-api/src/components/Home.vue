<template>
<div>
    <h1>{{ msg }}</h1>
    <h1>{{ token }}</h1>
    

    <a href="http://localhost:8888" class="btn btn-primary">Log in with Spotify</a>
</div>
</template>

<script src="//cdnjs.cloudflare.com/ajax/libs/handlebars.js/2.0.0-alpha.1/handlebars.min.js"></script>
<script src="http://code.jquery.com/jquery-1.10.1.min.js"></script>

<script>
export default {
  name: 'Home',
  props: {
    msg: String,
    token: String
  },
  // data: function(){
  //   return {
  //     tk: this.token
  //   }
  // },
  methods: {
    getHashParams: function () {
      var hashParams = {};
      var e, r = /([^&;=]+)=?([^&;]*)/g,
      q = window.location.hash.substring(1);
      while (e = r.exec(q)) {
        hashParams[e[1]] = decodeURIComponent(e[2]);
      }
      return hashParams;
    },
  },
  beforeMount(){
    this.token = this.getHashParams().access_token
  },
}
</script>

<style>

</style>