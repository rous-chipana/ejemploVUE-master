<template>
    <div class="row">
        <div class="col-md-12">
            <RouterLink class="btn btn-primary" to="/datos_crear">Agregar datos</RouterLink>
        </div>
        <div class="col-md-12">
            <div class="card">
                <div class="card-body">
                    <table class="table">
                        <thead>
                            <tr>
                                <th scope="col">apellido _y_nombre</th>
                                <th scope="col">domicilio_poblacion_provincia_codigopostal</th>
                                <th scope="col">fecha_y_pais_de_nacimiento</th>
                                <th scope="col">estudios_realizados</th>
                                <th scope="col">centro_de_procedencia</th>
                                <th scope="col">cursos_que_ha_repetido</th>
                                <th scope="col">asignaturas_pendientes</th>
                                <th scope="col">numero_de_apercibimiento</th>
                                <th scope="col">numero_de_parte</th>
                                <th scope="col">enfermedades_significativas_y_alergias</th>
                                <th scope="col">nombre_del_padre</th>
                                <th scope="col">nombre_de_la_madre</th>
                                <th scope="col">profesion</th>
                                <th scope="col">edad</th>
                                <th scope="col">profesion</th>
                                <th scope="col">edad</th>
                                <th scope="col">telefonos</th>
                                <th scope="col">telefonos</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="data in datos">
                                <td>{{ data.apellido_y_nombre }}</td>
                                <td>{{ data.domicilio_poblacion_provincia_codigopostal }}</td>
                                <td>{{ data.fecha_y_pais_de_nacimiento }}</td>
                                <td>{{ data.estudios_realizados }}</td>
                                <td>{{ data.centro_de_procedencia }}</td>
                                <td>{{ data.cursos_que_ha_repetido }}</td>
                                <td>{{ data.asignaturas_pendientes }}</td>
                                <td>{{ data.numero_de_apercibimiento }}</td>
                                <td>{{ data.numero_de_parte }}</td>
                                <td>{{ data.enfermedades_significativas_y_alergias }}</td>
                                <td>{{ data.nombre_del_padre }}</td>
                                <td>{{ data.nombre_de_la_madre }}</td>
                                <td>{{ data.profesion }}</td>
                                <td>{{ data.edad }}</td>
                                <td>{{ data.profesion }}</td>
                                <td>{{ data.edad }}</td>
                                <td>{{ data.telefonos }}</td>
                                <td>{{ data.telefonos }}</td>
                                <td>
                                    <RouterLink class="btn btn-success" :to="'/datos_editar/' + data.id">Editar</RouterLink>
                                    <button class="btn btn-danger" @click="eliminar(data.id)">Eliminar
                                    </button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import { collection, getDocs, query, where,deleteDoc,doc } from "firebase/firestore";
import { auth, db } from "../../firebaseConfig";

import { defineComponent } from 'vue';
export default defineComponent({
    data() {
        return {
            loadingDoc: false,
            datos: []
        }
    },

    methods: {
        async getUrls() {
            try {
                this.datos= []
                const q = query(
                    collection(db, "datos")
                );
                const querySnapshot = await getDocs(q);
                querySnapshot.forEach((doc) => {
                    // console.log(doc.id);
                    this.datos.push({
                        apellido_y_nombre: doc.data().apellido_y_nombre,
                        domicilio_poblacion_provincia_codigopostal: doc.data().domicilio_poblacion_provincia_codigopostal,
                        fecha_y_pais_de_nacimiento: doc.data().fecha_y_pais_de_nacimiento,
                        estudios_realizados: doc.data().estudios_realizados,
                        centro_de_procedencia: doc.data().centro_de_procedencia,
                        cursos_que_ha_repetido: doc.data().cursos_que_ha_repetido,
                        asignaturas_pendientes: doc.data().asignaturas_pendientes,
                        numero_de_apercibimiento: doc.data().numero_de_apercibimiento,
                        numero_de_partes: doc.data().numero_de_partes,
                        enfermedades_significativas_y_alergias: doc.data().enfermedades_significativas_y_alergias,
                        id: doc.id,
                        // ...doc.data()
                    });
                });
                // console.log(this.datos);
            } catch (error) {
                console.log(error);
            }
        },
        async eliminar(id) {
            try {
                const q = doc(db, "datos", id);
                const docRef = await deleteDoc(q);
                this.getUrls()
            } catch (error) {
                console.log(error);
            }
        },
    },
    mounted() {
        this.getUrls()
    }
})
</script>