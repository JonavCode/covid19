<template>
    <div>
        <vue-good-table
        :columns="columns"
        :rows="rows"
        :line-numbers="true"
        :row-style-class="rowStyleClassFn"
        :search-options="{
            enabled: true,
            placeholder: 'Buscar en la tabla',
        }"
        :pagination-options="{
            enabled: true,
            nextLabel: 'Siguiente',
            prevLabel: 'Atras',
            rowsPerPageLabel: 'Filas por página',
            ofLabel: 'de',
            pageLabel: 'pagina', // for 'pages' mode
            allLabel: 'Todo',
        }"/> 
    </div>
</template>
<script>

import axios from 'axios';
import { VueGoodTable } from 'vue-good-table';
import 'vue-good-table/dist/vue-good-table.css'

export default {
    data(){
        return {
            columns: [
                {
                    label: 'No',
                    field: 'id_de_caso',
                },
                {
                    label: 'Departamento',
                    field: 'departamento',
                },
                {
                    label: 'Ciudad',
                    field: 'ciudad_de_ubicaci_n',
                },
                {
                    label: 'Género',
                    field: 'sexo',
                },
                {
                    label: 'Tipo',
                    field: 'tipo',
                },
                {
                    label: 'Pais de Procedencia',
                    field: 'pa_s_de_procedencia',
                },
                {
                    label: 'Estado',
                    field: 'atenci_n',
                },
                {
                    label: 'Edad',
                    field: 'edad',
                },
                {
                    label: 'Fecha Diagnostico',
                    field: 'fecha_de_diagn_stico',
                   
                },
            ],
            rows: [
            ],
        };
    },
    mounted(){
        axios.get('https://www.datos.gov.co/resource/gt2j-8ykr.json').then(response => {
            
            response.data.map(function(dato){
                if(dato.sexo == "F"){
                    dato.sexo = "Femenino";
                }else if(dato.sexo == "M"){
                    dato.sexo = "Masculino"
                }
            
                return dato;
            });

            this.rows = response.data;
        });
    },
    methods: {
        rowStyleClassFn(row) {
            return row.edad == "60 a 69" ? 'green' : 'red';
        },
    },
    components: {
        VueGoodTable,
        axios,
    }
}
</script>
<style>
    .green{
        background-color: #7ACF76;
    }
</style>