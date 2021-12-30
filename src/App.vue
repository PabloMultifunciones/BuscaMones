<template>
  <div id="app">
    <div class="container">
      <div class = "row mb-4">

        <h1 class="text-center">BuscaMones</h1>
        <h3 class="text-center">Esriba el nombre del pokemon que desee buscar</h3>
        <div class="input-group mb-3">
          
          <input type="text" class="form-control" v-model="answer" placeholder="Ej: pikachu" aria-label="Recipient's username" aria-describedby="button-addon2">
          <div class="input-group-append">
            
            <button class="btn btn-outline" type="button" id="button-addon2" v-on:click="search">Buscar</button>
          </div>
        </div>
        <div class="col-12">
          <h4>Mas buscados: </h4>
          <button v-for="element,indice in link" :key="indice" class="btn btn-secondary m-1" id="button-addon2" :link="link" v-on:click="helper(link[indice])">{{link[indice]}}</button>
        </div>
        <Response :img="srcImg" :abilities="statsPokemon" v-if="exist"/>
        <div class="alert alert-danger m-2" v-else-if="exist==false" role="alert">
          
          No se encontro el pokemon / Posibles razones:
          <ul>
            <li>El pokemon no existe</li>
            <li>Tiene letras mayusculas</li>
            <li>Tiene caracteres especiales</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Response from './components/Response.vue'

export default {
  name: 'App',
  components: {
    Response
  },

  data(){
    return {
      answer: null,
      buscando: false,
      message: null,
      pokemon: null,
      exist: null,
      statsPokemon: null,
      srcImg: null,
      link:["pikachu","bulbasaur","venusaur","charmander","charmeleon","charizard","squirtle","wartortle","rattata","raichu","camerupt","celesteela","cherubi","chikorita","ditto","blitzle","boldore","mewtwo","kyogre","silvally","eternatus","mew","latias"]
    }
  },

  methods: {
    search(){
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.answer}`)
      .then(response => {
        if(response.status == 200){
          this.exist = true;
          return response.json();
        }else{
          this.exist = false;
          this.message = "No se encontro nada";
          throw "No se encontro nada";
        }
      })
      .then((response) => {
        this.statsPokemon = response.stats;
        this.srcImg = response.sprites.front_default;
      });
    },
    helper(pokemon){
      this.answer = pokemon;
      this.search();
    } 
  },
}

</script>

<style>
@import "./assets/css/bootstrap.min.css";
body{
  background-image: url('./assets/img/background.jpeg');
  background-repeat: no-repeat;
  background-size: cover;
  color: rgb(15, 15, 47);
}
#button-addon2{
  background-color: yellow;
  color: black;
  border: 0;
}
#button-addon2:hover{
  background-color: black;
  color: yellow;
}
</style>
