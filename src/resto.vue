<template>
    <div class="resto">
        <span v-if="showInput==false"> 
        {{resto.nom}}, {{resto.Cuisine}},{{resto.Tarif}},
        {{resto.rue}},{{resto.numero}},{{resto.codepostal}},{{resto.commune}}
    <button v-on:click="showInput=true">Modifier </button></span>

    <span v-if="showInput">
        <input type ="text" v-model ="resto.restaurant">
        <button v-on ="updateResto(resto)">Sauver</button>
        <button v-on:click="deleteTodo(todo.idtask)">Supprimer</button>
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

            deleteResto(resto){ 
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