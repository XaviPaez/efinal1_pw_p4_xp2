<template>
  <div class="contenedor-imagen">
    <img
      class="imagen2"
      v-if="!mostrarPokemon"
      src="../store/imagen2.png"
      alt="No se puede mostrar la imagen"
    />
    <img
      class="imagenPokemon"
      v-if="mostrarPokemon"
      :src="url"
      alt="no se puede mostrar imagen"
    />
  </div>
</template>

<script>
export default {
  props: {

    pokemonId:{
      type:Number,
      required:true
    },
 
    mostrarPokemon:{
      type: Boolean,
      required: true
    }
  },
  computed: {
    url() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
};
</script>

<style scoped>
.imagen2 {
  height: 300px;

  width: auto;
}
.imagenPokemon {
  margin-top: 50px;
  margin-right: 35px;
}
img {
  height: 200px;
  right: 40%;
}
.contenedor-imagen {
  height: 300px;
}
</style>>


