<template>
  <div id="app">
    <FormularioVue @nuevo-dato="agregarDato" />
    <TablaVue :datos="datos" />
  </div>
</template>

<script>
import FormularioVue from '@/components/FormularioVue.vue'
import TablaVue from '@/components/TablaVue.vue'

export default {
  name: 'App',
  components: {
    FormularioVue,
    TablaVue

  },

  data() {
    return {
      datos: []
    };
  },
  methods: {
    agregarDato(nuevoDato) {
      this.datos.push(nuevoDato);
    }
  }
};
</script>

<style>
</style>
