<template>
  <div>
    <v-parallax dark src="@/assets/bg_spotify.jpg" height="1000">
      <h1 class="text-center">{{ titulo }}</h1>

      <v-form id="form-spotify">
        <v-container dark>
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="busca"
                :counter="10"
                label="Shakira..."
                required
                placeholder="Pesquisar..."
              ></v-text-field>
            </v-col>

            <v-col class="d-flex" cols="12" md="4">
              <v-select
                :items="itensTipoBusca"
                v-model="valorTipoBusca"
                label="Tipo de Busca"
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

      <div>
        <v-data-table
          :headers="headers"
          :items="dados"
          item-key="id"
          class="elevation-1"
        >
          <template v-slot:no-data>
              Sem dados disponíveis
          </template>
        </v-data-table>
      </div>
    </v-parallax>
  </div>
</template>
<script>
export default {
  name: "Home",
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
        { text: "Faixa", value: "tracks" },
      ],
      valorTipoBusca: "",
      dados: [],
    };
  },
  computed: {
    headers() {
      return [
        { text: "Nome", value: "name" },
        { text: "Popularidade", value: "popularity" },
        { text: "Link", value: "external_urls.spotify" },
      ];
    },
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
            case "tracks":
              this.dados = response.artists.items;
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
</style>