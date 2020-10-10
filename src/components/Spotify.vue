<template>
  <div>
    <v-parallax class="bg-conteudo" height="1000">
      <div v-if="token">
        <h1 class="text-center">{{ titulo }}</h1>

        <v-form id="form-spotify">
          <v-container dark>
            <v-row>
              <v-col cols="12" md="4">
                <v-text-field
                  v-model="busca"
                  :counter="25"
                  required
                  placeholder="Pesquisar..."
                ></v-text-field>
              </v-col>

              <v-col class="d-flex" cols="12" md="4">
                <v-select
                  :items="itensTipoBusca"
                  v-model="valorTipoBusca"
                  label="Tipo de Busca"
                  required
                ></v-select>
              </v-col>
              <v-col>
                <v-btn
                  class="d-flex"
                  cols="12"
                  md="2"
                  color="secondary"
                  elevation="2"
                  style="margin-top: 20px"
                  v-on:click="pesquisar()"
                >
                  Pesquisar
                </v-btn>
              </v-col>
            </v-row>
          </v-container>
        </v-form>
        <Snackbar texto="Você está logado!" />

        <div>
          <Tabela :dados="dados" />
        </div>
      </div>
      <div v-else class="text-center">
        <v-btn color="secondary" elevation="2">
          <a href="http://localhost:8888/login" class="btn-spotify"
            >Login Spotify</a
          >
        </v-btn>
      </div>
    </v-parallax>
  </div>
</template>
<script>
import Tabela from "./Tabela";
import Snackbar from "./Snackbar";

export default {
  name: "Spotify",
  components: {
    Tabela,
    Snackbar
  },
  props: {
    titulo: String,
  },
  data: () => {
    return {
      resultado: [],
      token: "",
      busca: "",
      itensTipoBusca: [
        { text: "Álbum", value: "album" },
        { text: "Artista", value: "artist" },
        { text: "Playlist", value: "playlist" },
        { text: "Música", value: "track" },
      ],
      valorTipoBusca: "track",
      dados: [],
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
    pesquisar() {
      var myHeaders = new Headers({
        Authorization: `Bearer ${this.token}`,
        Accept: "application/json",
        "Content-Type": "application/json",
      });

      fetch(
        `https://api.spotify.com/v1/search?q=${this.busca}&type=${this.valorTipoBusca}`,
        {
          method: "GET",
          dataType: "Json",
          headers: myHeaders,
          credentials: "same-origin",
        }
      )
        .then((response) => {
          return response.json();
        })
        .then((response) => {
          switch (this.valorTipoBusca) {
            case "album":
              this.dados = response.albums.items;
              break;
            case "artist":
              this.dados = response.artists.items;
              break;
            case "playlist":
              this.dados = response.playlists.items;
              break;
            case "track":
              this.dados = response.tracks.items;
              break;
          }
        })
        .catch((response) => {
          console.log(response);
        });
    },
  },
  beforeMount() {
    this.token = this.getHashParams().access_token;
  },
};
</script>

<style>
  #form-spotify {
    background: #272727;
  }

  .btn-abrir-spotify{
    background: #1da14b !important;
  }

  .btn-abrir-spotify a{
    color: #FFF !important;
  }

  .bg-conteudo{
    background:linear-gradient(120deg, #1db954, #191414);
  }

</style>