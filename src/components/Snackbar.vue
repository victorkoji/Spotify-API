<template>
  <div class="text-center">
    <v-snackbar v-model="snackbar" :multi-line="multiLine" :top="true" :right="true">
      {{ texto }}

      <template v-slot:action="{ attrs }">
        <v-btn color="green" text v-bind="attrs" @click="snackbar = false">
          Fechar
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
export default {
  name: "Snackbar",
  props: {
    texto: String,
  },
  data: () => {
    return {
      multiLine: true,
      snackbar: true,
      timeout: 6000,
    };
  },
};
</script>

<style>
</style>