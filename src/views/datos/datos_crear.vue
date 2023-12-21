<template>
    <div class="row">
        <div class="col-md-12">
            <div class="card">
                <div class="card-body">
                    <div class="mb-3">
                        <label class="form-label">DATOS DEL ALUMNO/A</label>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">apellidos y nombre:</label>
                        <input v-model="datos.apellidos_y_nombre" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">domicilio,poblacion,provincia,codigo postal:</label>
                        <input v-model="datos.domicilio_poblacion_provincia_codigopostal" type="email" class="form-control">
                    </div>
                    <div class="row">
                        <div class="col-md-3">
                            <div class="mb-3">
                                <label class="form-label">fecha y pais de nacimiento:</label>
                                <input v-model="datos.fecha_y_pais_denacimiento" type="email" class="form-control">
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="mb-3">
                                <label class="form-label">estudios realizados:</label>
                                <input v-model="datos.estudios_realizados" type="email" class="form-control">
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-3">
                            <div class="mb-3">
                                <label class="form-label">centro de procedencia:</label>
                                <input v-model="datos.centro_de_procedencia" type="email" class="form-control">
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="mb-3">
                                <label class="form-label">cursos que ha repetido:</label>
                                <input v-model="datos.cursos_que_ha_repetido" type="email" class="form-control">
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-3">
                            <div class="mb-3">
                                <label class="form-label">asignaturas pendientes:</label>
                                <input v-model="datos.asignaturas_pendientes" type="email" class="form-control">
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="mb-3">
                                <label class="form-label">numero de apercibimiento:</label>
                                <label class="form-label">numero de partes:</label>
                                <input v-model="datos.numero_de_apercibimiento" type="email" class="form-control">
                            </div>
                        </div>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">enfermedades significativas y alergias:</label>
                        <input v-model="datos.enfermedades_significativas_y_alergias" type="email" class="form-control">
                    </div>
                </div>
            </div>
        </div>
        <div class="col-md-12">
            <button @click="guardar()" type="button" class="btn btn-primary">Guardar</button>
            <RouterLink class="btn btn-light" to="/datos_listar">Cancelar</RouterLink>
        </div>
    </div>
</template>
<script>

import { collection, getDocs, query, where,addDoc } from "firebase/firestore";
import { auth, db } from "../../firebaseConfig";
import { defineComponent } from 'vue';
export default defineComponent({
    // name: 'scanner',
    data() {
        return {
            loadingDoc: false,
            datos: {
                apellido_y_nombre: '',
                domicilio_poblacion_provincia_codigopostal: '',
                fecha_y_pais_de_nacimiento: '',
                estudios_realizados: '',
                centro_de_procedencia: '',
                cursos_que_ha_repetido: '',
                asignaturas_pendientes: '',
                numero_de_apercibimiento: '',
                numero_de_partes: '',
                enfermedades_significativas_y_alergias: ''
            },
        }
    },
    methods: {
        async guardar() {
            try {
                const q = query(collection(db, 'datos'));
                const docRef = await addDoc(q, this.datos);
                this.$router.push({ name: 'datos_listar' })
            } catch (error) {
                console.log(error);
            } 
        },
    },
    created() {
    }
})
</script>