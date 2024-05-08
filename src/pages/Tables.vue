<template>
    <div class="page-body"
        style="background-color: rgb(227,205,174); top: 10;left: 0;font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;">
        <center>
            <h1 class="text-2xl font-bold p-4"> Tablas de Estadisticas</h1>
        </center>
    </div>

    <div class=" flex justify-center">
        <div class="relative overflow-x-auto p-4">
            <table class="w-500 text-sm text-left text-gray-500 dark:text-gray-400">
                <caption style="background-color:rgb(94,94,94)" class="text-white">Estudiantes por Genero</caption>
                <thead class="text-s text-black" style="background-color: rgb(227,205,174);">
                    <tr>
                        <th scope="col" class="px-6 py-3">Genero</th>
                        <th scope="col" class="px-6 py-3">Total </th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            Femenino
                        </th>
                        <td class="px-6 py-4">
                            {{totalMujeres}}
                        </td>

                    </tr>
                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            Masculino
                        </th>
                        <td class="px-6 py-4">
                            {{totalHombres}}
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="relative overflow-x-auto p-4">
            <table class="w-500 text-sm text-left text-gray-500 dark:text-gray-400">
                <caption style="background-color:rgb(94,94,94)" class="text-white">Estudiantes por Edad</caption>
                <thead class="text-s text-black" style="background-color: rgb(227,205,174);">
                    <tr>
                        <th scope="col" class="px-6 py-3">Edad</th>
                        <th scope="col" class="px-6 py-3">Total </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(total, edad) in edades" :key="edad"
                        class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            {{ edad }} años
                        </th>
                        <td class="px-6 py-4">
                            {{ total }}
                        </td>
                    </tr>

                </tbody>
            </table>
        </div>

        <div class="relative overflow-x-auto p-4">
            <table class="w-500 text-sm text-left text-gray-500 dark:text-gray-400">
                <caption style="background-color:rgb(94,94,94)" class="text-white">Estudiantes por Numero de Control
                </caption>
                <thead class="text-s text-black" style="background-color: rgb(227,205,174);">
                    <tr>
                        <th scope="col" class="px-6 py-3">Numero de Control</th>
                        <th scope="col" class="px-6 py-3">Total de alumnos</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(total, numCtrl) in control" :key="numCtrl" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            {{ numCtrl }} ####
                        </th>
                        <td class="px-6 py-4">
                            {{ total}} 
                        </td>

                    </tr>
                    <!-- <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            2069####
                        </th>
                        <td class="px-6 py-4">
                            Total
                        </td>
                    </tr>

                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            2169####
                        </th>
                        <td class="px-6 py-4">
                            Total
                        </td>
                    </tr> -->
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";
const API =
    "https://raw.githubusercontent.com/DiegoMarqm/Estudiantes/main/students-20233.json";

export default {
    name: "TabEs",
    data() {
        return {
            // posts: [],
            estudiantes: [],
            edades: {},
            
            control: {},
        };
    },
    methods: {
        created() {
            // axios.get(API).then((response) => {
            //     this.posts = response.data;
            // });
            this.fetchData();

        },
        fetchData() {
            axios.get(API).then((response) => {
                this.estudiantes = response.data;
                this.totalEdades();
                this.contarNumeroCtrl();
            })
        },

        totalEdades() {
            this.edades = this.estudiantes.reduce((conteo, estudiantes) => {
                const edad = this.calcularEdad(estudiantes.dob);
                if (!conteo[edad]) {
                    conteo[edad] = 0;
                }
                conteo[edad]++;
                return conteo;
            }, {});
        },
        calcularEdad(fechaNacimiento) {
            const fechaHoy = new Date();
            const fechaNa = new Date(fechaNacimiento);
            const edad = fechaHoy.getFullYear() - fechaNa.getFullYear();
            const mes = fechaHoy.getMonth() - fechaNa.getMonth();

            if (mes < 0 || (mes === 0 && fechaHoy.getDate() < fechaNa.getDate())) {
                return edad - 1;
            }
            return edad;
        },

        contarNumeroCtrl(){
            this.control = this.estudiantes.reduce((contar, estudiantes) => {
                const numCtrl = estudiantes.email.substring(0, 4);
                if(!contar[numCtrl]){
                    contar[numCtrl] = 0;
                }
                contar[numCtrl]++;
                return contar;
            }, {});

        },

        contarxGenero(genero){
            return this.estudiantes.filter((estudiantes) => estudiantes.gender===genero).length;
        },

    },
    mounted() {
        this.created();
    },
    computed:{
        totalHombres(){
            return this.contarxGenero("male");
        },
        totalMujeres(){
            return this.contarxGenero("female");
        }
    }
};
</script>