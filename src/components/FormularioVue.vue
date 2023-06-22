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
              <field-messages name="nombre" show="$touched">
                <div slot="required">Debe ingresar el nombre</div>
              </field-messages>
            </validate>
        </div>

        <div class="form-group">
        <validate class="form-item f-item" tag="label">
          <input
            type="text"
            class="form-control"
            v-model="info.apellido"
            required
            name="apellido"
            placeholder="Ingrese Apellido"
          />
          <field-messages name="apellido" show="$touched">
            <div slot="required">Debe ingresar el apellido</div>
          </field-messages>
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
                min="18" max="99"
              />              
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
          <field-messages name="email" show="$touched">
            <div slot="required">Debe ingresar un Email</div>
          </field-messages>
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
            placeholder="Password"
          />
          <field-messages name="password" show="$touched">
            <div slot="required">La contraseña es requerida</div>
            <div slot="check-password">{{ info.passNivel }}
            </div>
          </field-messages>
        </validate>

        <div class="form-group">
            <validate class="form-item f-item" tag="label">
              <select
                type="text"
                class="form-control "
                v-model="info.rol"
                required
                name="rol"
                value="Usuario">
              <option disabled selected value style="display:none;">Seleccione un Rol</option>
              <option>Usuario</option>
              <option>Supervisor</option>
              <option>Administrador</option>
            </select>
              <small id="emailHelp" class="form-text text-muted">Campo es requerido</small>
            </validate>
        </div>

        
        </div>
        <b-button variant="outline-primary" type="submit">
          <b-icon icon="person-fill"></b-icon> Aceptar
        </b-button>
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
          edad: 18,
          email: "",
          password: "",
          passNivel: "",
          rol: "",
          msg: [],
        },
      };
    },
    methods: {
      agregarDato() {
        if (this.formstate.$valid) {
          this.$emit("nuevo-dato", { ...this.info }); 
          this.formstate['nombre'].$touched = false;
          this.info.nombre = "";
          this.formstate['apellido'].$touched = false;
          this.info.apellido = "";
          this.info.edad = 18;
          this.formstate['email'].$touched = false;
          this.info.email = "";
          this.formstate['password'].$touched = false;
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

  .text-muted{
    color: red;
  }
</style>
  