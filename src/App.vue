<template>
  <div id="app">
    <b-card class="p-5">
      <b-form>
        <div class="container">
          <div class="mb-3">
            <label for="nameInput">Ingresa tu nombre:</label>
            <b-form-input
              id="nameInput"
              v-model="name"
              placeholder="John Doe"
              type="text"
            ></b-form-input>
          </div>
          <div class="mb-3">
            <label for="ageInput">Ingresa tu edad:</label>
            <b-form-input
              id="ageInput"
              v-model="edad"
              placeholder="25"
              type="number"
            ></b-form-input>
          </div>
          <div class="mb-3">
            <label for="birthInput">Ingresa tu fecha de nacimiento:</label>
            <b-form-input
              id="birthInput"
              v-model="fechaNac"
              placeholder="01/05/1985"
              type="date"
            ></b-form-input>
          </div>
          <div class="mb-3">
            <label for="colorInput">Selecciona tu color favorito:</label>
            <b-form-input
              id="colorInput"
              v-model="favColor"
              type="color"
            ></b-form-input>
          </div>

          <div class="text-center">
            <b-button variant="dark" @click="validateInputs()">Enviar</b-button>
          </div>
        </div>
      </b-form>

      <div class="d-flex justify-content-center text-center mt-5">
        <b-alert show variant="danger" class="w-50" v-show="hasError">
          <h6 v-for="(campo, key) in camposError" :key="key">
            <strong
              >{{ campo }} es obligatorio! Revisa que lo hayas ingresado
              correctamente.</strong
            >
          </h6>
        </b-alert>
      </div>
      <!-- --- -->

      <div class="text-center mt-5">
        <b-table striped hover :items="items"></b-table>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      name: "",
      edad: "",
      fechaNac: "",
      favColor: "",
      items: [],
      camposError: [],
      hasError: false,
      canBeSent: false,
    };
  },
  methods: {
    validateInputs() {
      if (this.name === "") {
        this.hasError = true;
        setTimeout(() => (this.hasError = false), 2000);
        if (!this.camposError.includes("Nombre"))
          this.camposError.push("Nombre");
      }
      if (this.edad === "") {
        this.hasError = true;
        setTimeout(() => (this.hasError = false), 2000);
        if (!this.camposError.includes("Edad")) this.camposError.push("Edad");
      }
      if (this.fechaNac === "") {
        this.hasError = true;
        setTimeout(() => (this.hasError = false), 2000);
        if (!this.camposError.includes("Fecha de Nacimiento"))
          this.camposError.push("Fecha de Nacimiento");
      }
      if (this.favColor === "") {
        this.hasError = true;
        setTimeout(() => (this.hasError = false), 2000);
        if (!this.camposError.includes("Color")) this.camposError.push("Color");
      }
      //
      if (this.name && this.camposError.includes("Nombre")) {
        const index = this.camposError.indexOf("Nombre");
        if (index > -1) {
          this.camposError.splice(index, 1);
        }
      }
      if (this.edad && this.camposError.includes("Edad")) {
        const index = this.camposError.indexOf("Edad");
        if (index > -1) {
          this.camposError.splice(index, 1);
        }
      }
      if (this.fechaNac && this.camposError.includes("Fecha de Nacimiento")) {
        const index = this.camposError.indexOf("Fecha de Nacimiento");
        if (index > -1) {
          this.camposError.splice(index, 1);
        }
      }
      if (this.favColor && this.camposError.includes("Color")) {
        const index = this.camposError.indexOf("Color");
        if (index > -1) {
          this.camposError.splice(index, 1);
        }
      }
      if (this.camposError.length === 0) this.submitData();
    },
    submitData() {
      this.items.push({
        nombre: this.name,
        edad: this.edad,
        fecha_nacimiento: this.fechaNac,
        color_preferido: this.favColor,
      });
      this.emptyForm();
    },
    emptyForm() {
      this.name = "";
      this.edad = "";
      this.fechaNac = "";
      this.favColor = "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

@import "~bootstrap/dist/css/bootstrap.css";
</style>
