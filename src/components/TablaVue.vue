<template>
    <div class="table">
      <h2>Tabla</h2>
      <table class=" table-striped">
        <thead>
          <tr>
            <th scope="col">Nombre</th>
            <th scope="col">Apellido</th>
            <th scope="col">Edad</th>
            <th scope="col">Email</th>
            <th scope="col">Seguridad del Password</th>  
            <th scope="col">Rol en el sistema</th>      
          </tr>
        </thead>
        <tbody>
          <tr scope="row" v-for="(dato, index) in datos" :key="index">
            <td>{{ dato.nombre }}</td>
            <td>{{ dato.apellido }}</td>
            <td>{{ dato.edad }}</td>
            <td>{{ dato.email }}</td>
            <td>{{ dato.passNivel }}</td>
            <td>{{ dato.rol }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: "TablaDatos",
    props: {
      datos: {
        type: Array,
        default: () => [],
      },
    },
  };
  </script>
  
<style scoped>
.table{
    display: block;
    text-align: center;
    padding: 1rem 6rem;
}

.table-striped{
  align-items: cente;
}

</style>