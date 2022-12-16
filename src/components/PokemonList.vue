<template>
  <div class="list">
    <!--Ajout des pokemons visuellement -->
    <article v-for="donnees in this.donnees" v-bind:key="donnees.name" v-on:click = "showDetail(donnees)">
      <img :src="URL_IMG+donnees.name+'.png'" >
      <h3>{{donnees.name}}</h3>
    </article>
  </div>
</template>

<script>
// import de config à partir du fichier json 
import config from './../config/config.json';
// import d'axios pour faire une requete http
import axios from 'axios';
export default {
  data(){
    return{
      // Stocke les données des pokemons
      donnees : [],
      // On récupère l'url pour les images
      URL_IMG : config.IMG_URL,
    }
    
  },

  methods:{
    showDetail : function(donnees){
      this.$emit("PopUp",donnees);
    }
  },
  // Appel avant l'apparition du component
  beforeMount(){

      // appel de l'api pour récuperer la liste des characters
      axios.get(config.API_URL+'/pokemon')
      // sur le retour on stock la data dans this.donnees
      .then(data => (this.donnees = data.data.results))

      // En cas d'erreur
      .catch(error => console.log(error))

  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

