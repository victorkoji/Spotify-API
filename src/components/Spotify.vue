<template>
  <div>
    <v-parallax class="bg-conteudo" height="1000">
      <div v-if="user">
        <h1 class="text-center">{{ titulo }}</h1>

        <v-form id="form-spotify">
          <div v-if="error">
            <v-alert
              border="right"
              color="blue-grey"
              dark
            >
              {{error}}
            </v-alert>
          </div>
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
        <h1>Você não está logado!</h1>
        <ButtonLoginSpotify titulo="Login Spotify" />
        
      </div>
    </v-parallax>
  </div>
</template>
<script>
import Tabela from "./Tabela";
import Snackbar from "./Snackbar";
import ButtonLoginSpotify from "./ButtonLoginSpotify";

export default {
  name: "Spotify",
  components: {
    Tabela,
    Snackbar,
    ButtonLoginSpotify
  },
  props: {
    titulo: String,
    user: Object,
    token: String
  },
  data: () => {
    return {
      resultado: [],
      busca: "",
      valorTipoBusca: "track",
      dados: [],
      error: "",
      itensTipoBusca: [
        { text: "Álbum", value: "album" },
        { text: "Artista", value: "artist" },
        { text: "Playlist", value: "playlist" },
        { text: "Música", value: "track" },
      ]
    };
  },
  methods: {
    pesquisar() {
      var myHeaders = new Headers({
        Authorization: `Bearer ${this.token}`,
        Accept: "application/json",
        "Content-Type": "application/json",
      });

      /** Se o campo de pesquisar não estiver vazio, faz a busca **/
      /** Se estiver vazio, retorna uma mensagem de erro **/
      if(this.busca){
        this.error = ""; // Coloca vazio no campo de erro

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
      }else{
        this.error = 'O campo de busca está vazio!';
      }
    },
  }
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