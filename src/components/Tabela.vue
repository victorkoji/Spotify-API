<template>
  
</template>

<script>
export default {
  name: "Tabela",
  props: {
    dados: [],
  },
  data() {
    return {
      search: "",
      calories: ""
    }
  },
  computed: {
    headers() {
      return [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        {
          text: "Calories",
          value: "calories",
          filter: (value) => {
            if (!this.calories) return true;

            return value < parseInt(this.calories);
          },
        },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" },
      ];
    },
  },
  
};
</script>

<style>
</style>