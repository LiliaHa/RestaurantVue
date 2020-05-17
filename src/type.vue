<template>
    <div class="type">
        <span v-if="showInput==false"> 
        {{type.Cuisine}}
        <button v-on:click="showInput=true">Modifier </button></span>

        <span v-if="showInput == true">
            <div>
                <div>
                    <label for="nom">Nom du type :</label>
                    <input type="text" v-model="type.Cuisine">
                </div>
                
            </div>
            <button v-on:click="updateType(type)">Sauver</button>
            <button v-on:click="deleteType(type.idType)">Supprimer</button>
            <button v-on:click="showInput=false">Annuler</button>
        </span>
    </div>
</template>

<script>
    export default{

        name: 'Type',
        props: ['type'],
        data () {
            return{
                showInput:false
            }
        },

        methods: {
            updateType(type) {
                this.$emit('event_update',type);
                this.showInput = false;
            },

            deleteType(id){ 
                this.$emit('event_delete',id);
            },
        }
    }
</script>

<style>

.type{
    background-color:rgb(168, 209, 197);
    width: 300px;
    margin: 5px auto;
    padding : 5px;
}
</style>