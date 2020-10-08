<template>
<div>
    <h1>{{ msg }}</h1>
    <h1>{{ token }}</h1>

    <v-btn color="accent" elevation="2">
      <a href="http://localhost:8888" class="btn btn-primary">Login Spotify</a>
    </v-btn>

    <v-btn color="accent" elevation="2" style="margin-top:20px" v-on:click="topTracksLorde()">
      Pesquisar
    </v-btn>

    <p id="teste">{{ resultado }}</p>
</div>
</template>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.js" integrity="sha512-WNLxfP/8cVYL9sj8Jnp6et0BkubLP31jhTG9vhL/F5uEZmg5wEzKoXp1kJslzPQWwPT1eyMiSxlKCgzHLOTOTQ==" crossorigin="anonymous"></script>
<script>
export default {
  name: 'Home',
  props: {
    msg: String
  },
  data: () => {
    return{
      resultado: [],
      token: ""
    } 
  },
  methods: {
    getHashParams () {
      var hashParams = {};
      var e, r = /([^&;=]+)=?([^&;]*)/g,
      q = window.location.hash.substring(1);
      while (e = r.exec(q)) {
        hashParams[e[1]] = decodeURIComponent(e[2]);
      }
      return hashParams;
    },
    topTracksLorde() {
      this.token = this.getHashParams().access_token;

      var myHeaders = new Headers({
        'Authorization': `Bearer ${this.token}`, 
        'Accept': 'application/json',
        'Content-Type': 'application/json'
      })

      fetch('https://api.spotify.com/v1/artists/163tK9Wjr9P9DmM0AVK7lm/top-tracks?country=BR', {
        method: 'GET',
        dataType: "Json",
        headers: myHeaders,
        credentials: 'same-origin'
      })
      .then(response => {
        return response.json();
      })
      .then((response) => {
        this.resultado = response.tracks;
      })
      .catch((response) => {
        console.log(response)
      });
    }
  },
  beforeMount(){
    // this.token = this.getHashParams().access_token
  }
}
</script>

<style>

</style>