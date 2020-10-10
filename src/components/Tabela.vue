<template>
  <v-data-table
    :headers="headers"
    :items="dados"
    item-key="id"
    class="elevation-1 dados-tabela"
    :footer-props="{
      'items-per-page-text':'Itens por página'
    }"
  >
    <template v-slot:no-data> Sem dados disponíveis </template>
    <template v-slot:[`item.external_urls.spotify`]="{ value }">
      <v-btn elevation="2" class="btn-abrir-spotify">
        <a :href="`${value}`" target="_blank"> Abrir no spotify </a>
      </v-btn>
    </template>
  </v-data-table>
</template>

<script>
export default {
  name: "Tabela",
  props: {
    dados: Array,
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
};
</script>

<style>
  .dados-tabela .v-data-table__wrapper{
    max-height: 500px;
    overflow-y: auto;
  }
</style>