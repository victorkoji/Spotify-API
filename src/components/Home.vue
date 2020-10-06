<template>
<div>
    <h1>{{ msg }}</h1>
    <h1>{{ token }}</h1>
    

    <a href="http://localhost:8888" class="btn btn-primary">Log in with Spotify</a>
</div>
</template>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.js" integrity="sha512-WNLxfP/8cVYL9sj8Jnp6et0BkubLP31jhTG9vhL/F5uEZmg5wEzKoXp1kJslzPQWwPT1eyMiSxlKCgzHLOTOTQ==" crossorigin="anonymous"></script>
<script>
export default {
  name: 'Home',
  props: {
    msg: String
  },
  methods: {
    getHashParams: () => {
      var hashParams = {};
      var e, r = /([^&;=]+)=?([^&;]*)/g,
      q = window.location.hash.substring(1);
      while (e = r.exec(q)) {
        hashParams[e[1]] = decodeURIComponent(e[2]);
      }
      return hashParams;
    },
    topTracksLorde: () => {
      $.ajax({
        method: "GET",
        dataType: "Json",
        url:"https://api.spotify.com/v1/artists/163tK9Wjr9P9DmM0AVK7lm/top-tracks?country=BR",
        headers: {
          Authorization: `Bearer ${this.token}`
        },
        success: (response) => {
          console.log(response)
        },
        error: () => {}
      });
    }
  },
  beforeMount(){
    this.token = this.getHashParams().access_token
  },
  afterMount(){
    console.log(`adfhuasfhua`)
    this.topTracksLorde()
  }
}
</script>

<style>

</style>