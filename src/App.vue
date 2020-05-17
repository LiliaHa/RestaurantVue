 <template>
  <div id="app"> <h1> Repertoire de restaurants</h1>
    <Restolist></Restolist>
    <Typelist></Typelist>
  </div>
</template>

<script>
  import Restolist from './restolist'
  import Typelist from './typelist'
  export default {
  name: 'app',
  components: {Restolist,Typelist},
  data () {
    return {

      
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background-color: rosybrown;
  margin-top: 60px;
  padding: 60;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
