<template>
    <div class="container text-start">
        <h1 class="text-primary fw-bold">Edit</h1>
        <div class="card">
            <div class="card-header fw-bold">
                Pais
            </div>
            <div class="card-body">
                <form @submit.prevent="updatePais">

                    <div class="row mb-3">
                        <label for="pais_codi" class="form-label">Code</label>
                        <div class="input-group">
                            <div class="input-group-text"> <font-awesome-icon icon="tag" /> </div>
                            <input type="text" class="form-control" id="pais_codi" placeholder="Country code" disabled
                                v-model='pais.pais_codi' />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <label for="pais_nomb" class="form-label">Name:</label>
                        <div class="input-group">
                            <div class="input-group-text"> <font-awesome-icon icon="building" /> </div>
                            <input type="text" class="form-control" id="pais_nomb" placeholder="Country name"
                                v-model="pais.pais_nomb" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <label for="pais_capi" class="form-label">Capital:</label>
                        <div class="input-group">
                            <div class="input-group-text"> <font-awesome-icon icon="city" /> </div>
                            <input type="text" class="form-control" id="pais_capi" placeholder="Capital city"
                                v-model="pais.pais_capi" />
                        </div>
                    </div>

                    <button class="btn btn-primary" type="submit">Update</button>
                    <button class="btn btn-secondary mx-2" @click="cancel">Cancel</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
    name: 'EditarPais',
    data() {
        return {
            pais: {
                pais_codi: 0,
                pais_nomb: '',
                pais_capi: ''
            }
        }
    },
    methods: {
        cancel() {
            this.$router.push({ name: 'Paises' })
        },

        async updatePais() {
            const res = await axios.put(`http://127.0.0.1:8000/api/paises/${this.pais.pais_codi}`, this.pais)
            if (res.status === 200) {
                this.$router.push({ name: 'Paises' })
                Swal.fire({
                    position: 'top-end',
                    icon: 'success',
                    title: 'Country has been updated',
                    showConfirmButton: false,
                    timer: 2000
                })
            }
        }
    },

    mounted() {
        this.pais.pais_codi = this.$route.params.id
        axios.get(`http://127.0.0.1:8000/api/paises/${this.pais.pais_codi}`)
            .then(response => {
                this.pais = response.data.pais
            })
    },
}
</script>
