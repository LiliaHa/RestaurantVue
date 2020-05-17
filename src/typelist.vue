  
<template>
    <div id='typelist'>
        <h1> Mon repertoire de type</h1>

        <div>
            <label for="nom">Nom du type :</label>
            <input type="text" v-model="type.Cuisine">
        </div>
    
        <button v-on:click ="postType()">Save</button>

    <div v-for= "type in typelist" v-bind:key="type.idrestaurant">
         <Type v-bind:type="type" @event_update="update" @event_delete="deletetype"></Type>
    </div>
    
    </div>
</template>

<script>
    import axios from 'axios';
    import Type from "./type.vue";
    export default {
        components: {Type},
        name: 'Typelist',
        data() {
            return {

                type:{
                    Cuisine:"none",  
                    idType:0
                },

                typelist:[],
                url:"http://localhost:8000/api/type"
            }
        },
        methods: {
            get_typelist() {
                axios
                .get(this.url + "/list")
                .then((response) => {
                    this.typelist = response.data;
                    console.log(this.typelist);

                })
                .catch((error) =>  {
                    console.log(error);
                
                })
                
            },
            postType () {
                axios.post(this.url+"/add",this.type)
                .then((response) => {
                    console.log(response.data);
                    this.get_typelist();
                })

                .catch ((error) => {
                    console.log(error);
                })
            },
            update(type) {
                axios.put(this.url + "/update/" + type.idType,type)
                .then((response) =>{console.log(response.data);
                })
                .catch((error) => {
                    console.log(error);

                })
            },
            deletetype(id) {
                axios.delete(this.url+ "/delete/" + id)
                .then((response) => {
                    this.get_typelist();
                    console.log(response.data);
                })
            }

        },

        mounted () {
            this.get_typelist();
        }
    }
</script>

<style >

#typelist {

    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
    background-color: rgb(105, 141, 241);
    margin: 60px auto;
    padding: 100px;
    width: 500px;
}
    
</style>