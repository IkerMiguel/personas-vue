<template>
  <div class="container">
    <h1 class="text-start">Listado Departamentos |
      <button @click="newDepartamento" class="btn btn-success mx-2">
        <font-awesome-icon icon="plus" />
      </button>
    </h1>
    <table class="table">
      <thead>
        <tr>
          <th class="col">#</th>
          <th class="col">Code</th>
          <th class="col">Name</th>
          <th class="col">Country</th>
          <th class="col">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(departamento, index) in departamentos" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ departamento.depa_codi }}</td>
          <td>{{ departamento.depa_nomb }}</td>
          <td>{{ departamento.pais_nomb }}</td>
          <td>
            <button @click="deleteDepartamento(departamento.depa_codi)" class="btn btn-danger mx-2">
              <font-awesome-icon icon="trash" />
            </button>
            <button @click="editDepartamento(departamento.depa_codi)" class="btn btn-warning mx-2">
              <font-awesome-icon icon="pencil" />
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
  name: 'Departamento',
  data() {
    return {
      departamentos: []
    }
  },
  methods: {
    
  },
  mounted() {
    axios.get('http://127.0.0.1:8000/api/departamentos')
      .then(response => (this.departamentos = response.data.departamentos))
  }
}
</script>
