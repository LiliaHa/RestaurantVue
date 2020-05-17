  
<template>
    <div id='restolist'>
        <h1> Mon repertoire de restaurants</h1>

        <div>
            <label for="nom">Nom du restaurant :</label>
            <input type="text" v-model="resto.nom">
        </div>
        <div>
            <label for="rue">Type de Cuisine :</label>
            <input type="text" v-model="resto.TypeDeCuisine">
            
        </div>
        <div>
            <label for="rue">Tarif :</label>
            <input type="text" v-model="resto.tarif">
        </div>
        <div>
            <label for="rue">Nom de la rue :</label>
            <input type="text" v-model="resto.rue">
        </div>
        <div>
            <label for="rue">Numero de rue:</label>
            <input type="number" v-model="resto.numero">
        </div>
        <div>
            <label for="rue">Code Postal :</label>
            <input type="number" v-model="resto.codepostal">
        </div>
        <div>
            <label for="rue">Commune :</label>
            <input type="text" v-model="resto.commune">
        </div>
        <button v-on:click ="postResto()">Save</button>

    <div v-for= "resto in restolist" v-bind:key="resto.idrestaurant">
         <Resto v-bind:resto="resto" @event_update="update" @event_delete="deleteResto"></Resto>
    </div>
    
    </div>
</template>

<script>
    import axios from 'axios';
    import Resto from "./resto.vue";
    export default {
        components: {Resto},
        name: 'Restolist',
        data() {
            return {

                resto:{
                    TypeDeCuisine :0,
                    Cuisine:"none",
                    codepostal:0,
                    commune:"none",
                    adresse :0,
                    idrestaurant:0,
                    idType:0,
                    nom:"none",
                    numero:0,
                    rue:"none",
                    tarif:"none",
                },

                restolist:[],
                url:"http://localhost:8000/api/restaurant"
            }
        },
        methods: {
            get_restolist() {
                axios
                .get(this.url + "/list")
                .then((response) => {
                    this.restolist = response.data;
                    console.log(this.restolist);

                })
                .catch((error) =>  {
                    console.log(error);
                
                })
                
            },
            postResto () {
                axios.post(this.url+"/add",this.resto)
                .then((response) => {
                    console.log(response.data);
                    this.get_restolist();
                })

                .catch ((error) => {
                    console.log(error);
                })
            },
            update(resto) {
                axios.put(this.url + "/update/" + resto.idRestaurant,resto)
                .then((response) =>{console.log(response.data);
                })
                .catch((error) => {
                    console.log(error);

                })
            },
            deleteResto(id) {
                axios.delete(this.url+ "/delete/" + id)
                .then((response) => {
                    this.get_restolist();
                    console.log(response.data);
                })
            }

        },

        mounted () {
            this.get_restolist();
        }
    }
</script>

<style >

#restolist {

    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
    background-color: rgb(241, 105, 105);
    margin: 60px auto;
    padding: 100px;
    width: 500px;
}
    
</style>