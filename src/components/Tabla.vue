<template>
  <v-data-table
    :headers="headers"
    :items="personal"
    :items-per-page="5"
    class="elevation-1"
    :loading="'!=personal.length'"
    loading-text="Cargando...Por favor espere!"
  >
    <template v-slot:item.bono="{ item }">
      <v-chip :color="getColor(item.bono)" dark>
        {{ item.bono | bonos }}
      </v-chip>
    </template>
    <template v-slot:item.sueldo="{ item }" >
      
        {{ item.sueldo | decimalNumer }}
      
    </template>
  </v-data-table>
</template>

<script>
export default {
  props: {
    personal: Array,
  },
  data() {
    return {
      loadTable: true,
      headers: [
        {
          text: "Colaborador",
          align: "start",
          sortable: false,
          value: "nombre",
        },
        { text: "Fecha Ingreso", value: "fecha" },
        { text: "Sis Pension", value: "pension" },
        { text: "Sexo", value: "sexo" },
        { text: "Bono", value: "bono" },
        { text: "Sueldo", value: "sueldo",align: 'right' },
      ],
    };
  },
  methods: {
    getColor(bono) {
      if (bono) return "green";
      else return "red";
    },
  },
  filters: {
    bonos(value) {
      return value ? "Si" : "No";
    },
    decimalNumer(value) {
      return value.toFixed(2);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>