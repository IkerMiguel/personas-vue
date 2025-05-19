<template>
  <div class="container">
    <h1 class="text-start">Lista de Paises |
      <button @click="newPais" class="btn btn-success mx-2">
        <font-awesome-icon icon="plus" />
      </button>
    </h1>
    <table class="table">
      <thead>
        <tr>
          <th class="col">#</th>
          <th class="col">Code</th>
          <th class="col">Name</th>
          <th class="col">Capital</th>
          <th class="col">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(pais, index) in paises" :key="pais.pais_codi">
          <td scope="row">{{ index + 1 }}</td>
          <td>{{ pais.pais_codi }}</td>
          <td>{{ pais.pais_nomb }}</td>
          <td>{{ pais.pais_capi }}</td>
          <td>
            <button @click="deletePais(pais.pais_codi)" class="btn btn-danger mx-2">
              <font-awesome-icon icon="trash" />
            </button>
            <button @click="editPais(pais.pais_codi)" class="btn btn-warning mx-2">
              <font-awesome-icon icon="pencil" />
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import Swal from 'sweetalert2'

export default {
  name: 'Pais',
  data() {
    return {
      paises: []
    }
  },
  methods: {
    deletePais(code) {
      Swal.fire({
        title: `Do you want to delete the country with code ${code}?`,
        showCancelButton: true,
        confirmButtonText: 'Delete',
      }).then((result) => {
        if (result.isConfirmed) {
          axios.delete(`http://127.0.0.1:8000/api/paises/${code}`)
            .then(response => {
              if (response.data.success) {
                Swal.fire('Deleted!', '', 'success')
                this.paises = response.data.paises
              }
            })
        }
      })
    },
  },
  mounted() {
    axios
      .get('http://127.0.0.1:8000/api/paises')
      .then(response => (this.paises = response.data.paises))
  },
}
</script>
