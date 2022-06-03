<template>
  <div id="app">
    
    <div class="container">
      <PokeCard></PokeCard>
    </div>
  </div>
</template>

<script>
import PokeCard from "./components/PokeCard.vue";
export default {
  name: "App",
  created() {
    document.title = "Poke Alfa";
  },
  components: {
    PokeCard,
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
}
#app {
  background: #e3dfdf	
    no-repeat center center fixed !important;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover !important;
  background-position: center;
  min-height: 100vh;

  }

</style>