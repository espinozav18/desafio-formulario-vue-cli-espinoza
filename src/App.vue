<template>
  <v-app>
    <MenuBar />

    <v-main>
      <v-card>
        <v-card-title>Registro de datos</v-card-title>
        <v-card-text>
          <v-row>
            <v-col :class="'ma-3'">
              <Formulario   @datosPersonal="cargarDatos($event)"/>
            </v-col>
            <v-col>
              <Tabla
                :personal="dpersonal"
               
              />
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
import Formulario from "./components/Formulario.vue";
import MenuBar from "./components/MenuBar.vue";
import Tabla from "./components/Tabla.vue";
export default {
  name: "App",
  components: {
    MenuBar,
    Formulario,
    Tabla,
  },

  data() {
    return { dpersonal: [] };
  },
  methods: {
    cargarDatos(personal) {
      this.dpersonal.push(personal);
    },
    
  },
};
</script>
