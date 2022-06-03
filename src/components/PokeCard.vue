<template>
  <div class="container">
    <input
      type="text"
      name="nome"
      value=""
      placeholder="Search"
      v-model="pesquisa"
      />
      <div class="card">
      <ul v-for="pokemon in filtro" :key="pokemon">
       <li>  
          <div class="imagem">             
           <img
            :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getImg(
              pokemon
            )}.png`"
            alt="pokemon.name"
            />
           </div>  
           <div class="paragrafo"> 
           <p>
             {{ caseUp(pokemon) }}
           </p> 

           <p><span>#</span>{{ getImg(pokemon) }}</p> 

           </div>         
             
        </li>     
      </ul>     
    </div>
    </div>
 
</template>

<script>
import axios from "axios";
export default {
  name: "PokeCard",
  data() {
    return {
      titulo: "PokeDex",
      pokemons: [],
      pokeInfo: null,
      modal: false,
      pesquisa: "",
    };
  },
  mounted() {
    axios
      .get("https://pokeapi-215911.firebaseapp.com/api/v2/pokemon?limit=151")
      .then((response) => {
        this.pokemons = response.data.results;
        this.modal = true;
      });
  },
  computed: {
    filtro() {
      return this.pokemons.filter((i) => {
        return i.name.includes(this.pesquisa);
      });
    },
  },
  methods: {
    getImg(pokemon) {
      return pokemon.url.split("/")[6];
    },
    caseUp(pokemon) {
      return pokemon.name
        .charAt(0)
        .toUpperCase()
        .concat(pokemon.name.substring(1));
    },
    handleInfo(id) {
      axios
        .get(`https://pokeapi-215911.firebaseapp.com/api/v2/pokemon/${id}`)
        .then((response) => {
          this.pokeInfo = response.data;
        });
      window.scrollTo({
        top: 0,
        behavior: "smooth",
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");

.card{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
    padding: 20px;
    
}

.card ul{
  background-color: aliceblue;
  max-width: 200px;
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  border-radius: 4px;
  box-shadow: 5px 5px 5px 2px rgb(208, 207, 216);
}

.card li{
  display: flex;
  align-items: center;
  flex-direction: column;
}

.paragrafo{
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 95px;
  padding-bottom: 1rem;
  margin: 0 2rem;
  font-size: 12px;
  font-family: Arial, Helvetica, sans-serif;
}

input {
    margin: 20px;
    margin-bottom: -10px;
    padding: 5px;
    width: 94.5vw;
    border: #ccc;
    color: black;
    background-color: #f3efef; 
    border-radius: 4px; 
    border-style: none;
    outline: none;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1rem;        
}
</style>
   
