<template>
  <v-form ref="form" v-model="valid" lazy-validation>
    <v-row align="center">
      <v-col class="d-flex" cols="12" sm="9">
        <v-text-field
          v-model.trim="personal.nombre"
          :rules="nombreRules"
          label="Nombre del trabajador"
          required
        ></v-text-field>
      </v-col>
      <v-col class="d-flex" cols="12" sm="3">
        <v-text-field
          v-model="personal.fecha"
          :rules="[(v) => !!v || 'Fecha es requerido']"
          type="date"
          label="Fecha Ingreso"
          required
        ></v-text-field>
      </v-col>
    </v-row>

    <v-row align="center">
      <v-col class="d-flex" cols="12" sm="6">
        <v-select
          v-model="personal.pension"
          :items="items"
          :rules="[(v) => !!v || 'Pension es requerido']"
          label="Sistema de pensiones"
          required
        ></v-select>
      </v-col>
      <v-col class="d-flex" cols="12" sm="6">
        <v-radio-group
          v-model="personal.sexo"
          row
          :rules="[(v) => !!v || 'Es requerido']"
        >
          <template v-slot:label>
            <div><strong>Sexo</strong></div>
          </template>
          <v-radio
            v-for="(s, i) in sexoItem"
            :key="i"
            :label="s.descripcion"
            :value="s.value"
          ></v-radio>
        </v-radio-group>
      </v-col>
    </v-row>
    <v-row align="center">
      <v-col class="d-flex" cols="12" sm="6">
        <v-checkbox v-model="personal.bono" label="Recibe bono?"></v-checkbox>
      </v-col>
      <v-col class="d-flex" cols="12" sm="6">
        <v-text-field
          v-model.number="personal.sueldo"
          :rules="[(v) => !!v || 'Sueldo es requerido']"
          :type="'number'"
          label="Sueldo"
          required
        ></v-text-field>
      </v-col>
    </v-row>

    <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
      Registrar
    </v-btn>

    <v-btn color="error" class="mr-4" @click="reset"> Limpiar</v-btn>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    personal: {
      nombre: "",
      fecha: "",
      pension: "",
      sexo: "",
      bono: false,
      sueldo: 0.0,
    },

    sexoItem: [
      { value: "M", descripcion: "Masculino" },
      { value: "F", descripcion: "Femenino" },
    ],

    nombreRules: [(v) => !!v || "Nombre es requerido"],
    items: [
      "Sistema Nacional Pensiones (ONP)",
      "SPS - Habitat",
      "SPS - Integra",
      "SPS - Profuturo",
    ],
  }),

  methods: {
    validate() {
      const validar = this.$refs.form.validate();
      if (validar) {
        this.$emit("datosPersonal", this.personal);
        this.personal = {
          nombre: "",
          fecha: "",
          pension: "",
          sexo: "",
          bono: false,
          sueldo: 0.0,
        };
        this.$refs.form.reset();
      }
    },
    reset() {
      this.$refs.form.reset();
    },
  },
};
</script>

<style lang="scss" scoped>
</style>