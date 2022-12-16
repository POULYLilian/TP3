<template>
  <div class="container">
    <PokemonSearch />
    <PokemonDetail 
    v-if="visible"
    v-on:PokemonBox = "closeDetail"
    :pokemonUrl= "this.pokemonUrl"
    />
    <PokemonList 
    v-on:PopUp = "openDetail"/>
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
  data(){
    return{
      // Visibilité du pop up initialisé à faux (invisible)
      visible : false,
    }
  },
  methods:{
    openDetail : function(donnees) {
      this.pokemonUrl = donnees.url,
      // Fait apparaitre le pop up
      this.visible = true;
    },
    closeDetail : function(){
      // Fait disparaître le pop up
      this.visible = false;
    }
  }
};

</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>