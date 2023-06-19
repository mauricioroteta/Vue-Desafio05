<template>
    <div class="card">
      <h2>Formulario</h2>

      <div>

      <vue-form
        class="form-group"
        :state="formstate"
        @submit.prevent="agregarDato"
      >
        <div class="form-group">
            <validate class="form-item f-item" tag="label">
              <input
                type="text"
                class="form-control "
                v-model="info.nombre"
                required
                name="nombre"
                placeholder="Ingrese Nombre"
              />
              <small id="emailHelp" class="form-text text-muted">Campo Requrido </small>
            </validate>
        </div>

        <div class="form-group">
        <validate class="form-item f-item" tag="label">
          <input
            type="text"
            class="form-control"
            v-model="info.apellido"
            required
            name="name"
            placeholder="Ingrese Apellido"
          />
          <small id="emailHelp" class="form-text text-muted">Campo Requrido </small>
        </validate>
        </div>

        <div class="form-group">
            <validate class="form-item f-item" tag="label">
              <input
                type="number"
                class="form-control "
                v-model="info.edad"
                required
                name="edad"
                placeholder="Ingrese Edad"
              />
              <small id="emailHelp" class="form-text text-muted">Campo Requrido </small>
            </validate>
        </div>

        <div class="form-group">
        <validate class="form-item f-item" tag="label">
          <input
            type="email"
            class="form-control"
            v-model="info.email"
            required
            name="email"
            placeholder="Ingrese EMail"
          /> 
          <small id="emailHelp" class="form-text text-muted">Campo Requrido </small>
        </validate>
       </div>

        <div class="form-group">  
        <validate
          class="form-item f-item" 
          tag="label"
          :custom="{'check-password': checkPassword}"
        >
          <input
            type="password"
            class="form-control"
            v-model="info.password"
            name="password"
            required
          />
          <small id="emailHelp" class="form-text text-muted">Campo Requrido </small>
        </validate>

        <div class="form-group">
            <validate class="form-item f-item" tag="label">
              <select
                type="text"
                class="form-control "
                v-model="info.rol"
                required
                name="rol"
                placeholder="Rol">
              <option>Usuarios</option>
              <option>supervisor</option>
              <option>Administrador</option>
            </select>
              <small id="emailHelp" class="form-text text-muted">Campo es requerido</small>
            </validate>
        </div>

        
        </div>
        <button type="submit">Agregar</button>
      </vue-form>
    </div>
    </div>
  </template>

  <script>
  export default {
    name: "FormularioVue",
    data() {
      return {
        formstate: {},
        info: {
          nombre: "",
          apellido: "",
          edad: 0,
          email: "",
          password: "",
          passNivel: "",
          rol: "",
        },
      };
    },
    methods: {
      agregarDato() {
        if (this.formstate.$valid) {
          this.$emit("nuevo-dato", { ...this.info }); 
          this.info.nombre = "";
          this.info.apellido = "";
          this.info.edad = 0;
          this.info.email = "";
          this.info.password = "";
          this.info.PassNivel = "";
          this.info.rol = "";
        }
      },
      
      checkPassword(password) {
        // Initialize variables
        var strength = 0;
        var tips = "";

        // Check password length
        if (password.length < 8) {
          tips += "- El password es muy corto ";
        } else {
          strength += 1;
        }

        // Check for mixed case
        if (password.match(/[a-z]/) && password.match(/[A-Z]/)) {
          strength += 1;
        } else {
          tips += "- Utilice mayusculas y minusculas ";
        }

        // Check for numbers
        if (password.match(/\d/)) {
          strength += 1;
        } else {
          tips += "- Incluya numeros ";
        }

        // Check for special characters
        if (password.match(/[^a-zA-Z\d]/)) {
          strength += 1;
        } else {
          tips += "- Incluya al menos un caracer especial";
        }

        // Return results
        if (strength < 2) {
          this.info.passNivel = "INSEGURA! " + tips;
          return this.info.passNivel;
        } else if (strength === 2) {
          this.info.passNivel = "MEDIA " + tips;
          return this.info.passNivel;
        } else if (strength === 3) {
          this.info.passNivel = "SEGURA. " + tips;
          return this.info.passNivel;
        } else {
          this.info.passNivel = "MUY SEGURA " + tips;
          return this.info.passNivel;
        }
      }

    },
    
  };


</script>

<style scoped>

html, body {
    height: 100%;
    margin: 0;
}


.card {
    display: block;
    text-align: center;
    padding: 1rem 15rem;
}

.f-item {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding-bottom: 10px;
  }
</style>
  