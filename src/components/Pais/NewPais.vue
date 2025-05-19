<template>
    <div class="container text-start">
        <h1 class="text-primary fw-bold">New</h1>
        <div class="card">
            <div class="card-header fw-bold">
                Pais
            </div>
            <div class="card-body">
                <form @submit.prevent="savePais">
                    <div class="row mb-3">
                        <label for="pais_codi" class="form-label">Code</label>
                        <div class="input-group">
                            <div class="input-group-text"><font-awesome-icon icon="tag" /></div>
                            <input type="text" class="form-control" id="pais_codi" placeholder="Country code"
                                v-model="pais.pais_codi" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <label for="pais_nomb" class="form-label">Name:</label>
                        <div class="input-group">
                            <div class="input-group-text"><font-awesome-icon icon="building" /></div>
                            <input type="text" class="form-control" id="pais_nomb" placeholder="Country name"
                                v-model="pais.pais_nomb" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <label for="pais_capi" class="form-label">Capital:</label>
                        <div class="input-group">
                            <div class="input-group-text"><font-awesome-icon icon="city" /></div>
                            <input type="text" class="form-control" id="pais_capi" placeholder="Capital city"
                                v-model="pais.pais_capi" />
                        </div>
                    </div>

                    <button class="btn btn-primary" type="submit">Save</button>
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
    name: 'NewPais',
    data() {
        return {
            pais: {
                pais_codi: '',
                pais_nomb: '',
                pais_capi: ''
            }
        }
    },
    methods: {
        cancel() {
            this.$router.push({ name: 'Paises' })
        },

        async savePais() {
            const res = await axios.post(`http://127.0.0.1:8000/api/paises/`, this.pais)
            if (res.status === 200) {
                this.$router.push({ name: 'Paises' })
                Swal.fire({
                    position: 'top-end',
                    icon: 'success',
                    title: 'Country has been saved',
                    showConfirmButton: false,
                    timer: 2000
                })
            }
        }
    }
}
</script>
