<template>
    <div class="resto">
        <span v-if="showInput==false"> 
        {{resto.nom}}, {{resto.Cuisine}},{{resto.Tarif}},
        {{resto.rue}},{{resto.numero}},{{resto.codepostal}},{{resto.commune}}
        <button v-on:click="showInput=true">Modifier </button></span>

        <span v-if="showInput == true">
            <div>
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
                    <input type="text" v-model="resto.Tarif">
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
            </div>
            <button v-on:click="updateResto(resto)">Sauver</button>
            <button v-on:click="deleteResto(resto.idRestaurant)">Supprimer</button>
            <button v-on:click="showInput=false">Annuler</button>
        </span>
    </div>
</template>

<script>
    export default{

        name: 'Resto',
        props: ['resto'],
        data () {
            return{
                showInput:false
            }
        },

        methods: {
            updateResto(resto) {
                
                this.$emit('event_update',resto);
                this.showInput = false;
            },

            deleteResto(id){ 
                this.$emit('event_delete',id);
            },
        }
    }
</script>

<style>

.resto{
    background-color:lightgrey;
    width: 300px;
    margin: 5px auto;
    padding : 5px;
}
</style>