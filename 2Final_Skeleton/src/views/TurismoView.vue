<template>
    <img src="../assets/euskadi-blanco.jpg" alt="Basque Tour">


    <select name="provincia" id="provincia" v-model="provincia">
    <option value="">Todas</option>
     <option v-for="(territorios, index) in provincias" :key="index" :value=territorios>{{ territorios }}</option>
    </select>

    <select name="mes" id="mes" v-model="mesus">
    <option value="">Todas</option>
     <option v-for="(mesex, index) in meses" :key="index" :value=mesex>{{ mesex }}</option>
    </select>

    <table>

        <tr>
            <th>Evento</th>
            <th>Fecha</th>
            <th>Territorio</th>
            <th>Descripcion</th>
            <th>Mas info</th>
            <th>Favoritos</th>
        </tr>

        <tr v-for="(agendas, index) in filtrar" :key="index" :class="{'Bizkaia':agendas.territory == 'Bizkaia', 'Araba':agendas.territory == 'Araba', 'Gipuzkoa':agendas.territory == 'Gipuzkoa', 'todos':agendas.territory == 'Araba Bizkaia Gipuzkoa', 'todes':agendas.territory == 'Bizkaia Araba Gipuzkoa'}">
                <td>{{ agendas.documentName }}</td>
                <td>{{ agendas.eventStartDate }}</td>
                <td>{{ agendas.territory }}</td>
                <td>{{ agendas.documentDescription }}</td>
                <td>{{ agendas.friendlyUrl }}</td>
                <td><button>Añadir</button></td>
        </tr>

    </table>
</template>

<script>

import axios from 'axios';

export default {
    name: 'TurismoView',

    data() {

        return {

            agenda: [],
            provincia: "",
            mesus: "",
            provincias:[],
            meses : ['Enero','Febrero','Marzo','Abril','Mayo','Junio','Julio','Agosto','Septiembre','Octubre', 'Noviembre','Diciembre'],

        }

    },

    mounted() {

        axios.get('json/agenda.json')
            .then((response) => {
                this.agenda = response.data;
                this.agenda.forEach(element => {
                    if(!this.provincias.includes(element.territory)){
                        this.provincias.push(element.territory);
                    }
                });
            })
            .catch((error) => {
                console.log(error);
            });


    },

    computed:{


        filtrar(){


            return this.agenda
            .filter(dato => {
               

                if (this.mesus === ''){
                    return this.agenda;
                }else{
                    let mex = dato.eventStartDate.split('/')[1];
                    let mesIndex = this.meses.indexOf(this.mesus);
                    return mex == mesIndex+1;

                }
            })
            .filter(dato => {
                if (this.provincia === '') {
                    return this.agenda;
                } else {
                    return dato.territory.includes(this.provincia);
                    
                }
            });
            

        }


    },


    methods:{


       



    }



}


</script>



<style>


.Gipuzkoa{

background-color: lightblue;

}

.Bizkaia{

background-color: lightgreen;

}

.Araba{


    background-color: lightsalmon;


}

.todos{

background-color: rgb(209, 209, 16);

}

.todes{

background-color: rgb(209, 209, 16);

}


</style>