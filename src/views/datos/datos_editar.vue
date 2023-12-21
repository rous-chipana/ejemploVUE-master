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
                    <div class="mb-3">
                        <label class="form-label">fecha y pais de nacimiento:</label>
                        <input v-model="datos.fecha_y_pais_denacimiento" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">estudios realizados:</label>
                        <input v-model="datos.estudiosrealizados" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">centro de procedencia:</label>
                        <input v-model="datos.centro_de_procedencia" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">cursos que ha repetido:</label>
                        <input v-model="datos.cursos_que_ha_repetido" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">asignaturas pendientes:</label>
                        <input v-model="datos.asignaturas_pendientes" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">numero de apercibimiento:</label>
                        <input v-model="datos.numero_de_apercibimiento" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">numero de partes:</label>
                        <input v-model="datos.numero_de_partes" type="email" class="form-control">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">enferrmedades significativas y alergias:</label>
                        <input v-model="datos.enfermedades_significativas_y_alergias" type="email" class="form-control">
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-3">
                        <img src="imagenes/rosmery.jpg" width="200" class="rounded mx-auto d-block" alt="...">
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

import { collection, getDocs,getDoc, query, where, addDoc, updateDoc, doc } from "firebase/firestore";
import { auth, db } from "../../firebaseConfig";
import { defineComponent } from 'vue';
export default defineComponent({
    data() {
        return {
            id: this.$route.params.id,
            datos: {
                apellido_y_nombre: '',
                domicilio, poblacion, provincia, codigo_postal: '',
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
        async getUrls() {
            try {
                const q = doc(db, "datos", this.id);
                const respuesta = await getDoc(q);
                this.datos=respuesta.data()
            } catch (error) {
                console.log(error);
            }
        },
        async guardar() {
            try {
                const q = doc(db, 'datos',this.id);
                const docRef = await updateDoc(q,this.datos);
                this.$router.push({ name: 'datos_listar' })
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.getUrls()
    }
})
</script>