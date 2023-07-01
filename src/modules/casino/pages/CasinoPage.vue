<template>
  <h1 v-if="puntaje < 10 && contador < 5">Juego Casino</h1>

  <div v-if="puntaje < 10 && contador < 5" class="container">
    <h1>
      Puntaje: <label for="">{{ puntaje }} </label> Intentos:
      <label for="">{{ contador }} </label>
    </h1>
  </div>

  <div v-if="puntaje < 10 && contador < 5" class="container">
    <div class="imagen">
      <PokemonImg :pokemonId="id1" :mostrarPokemon="mostrar" />
      <label class="nombre" for="">{{ nombre1 }}</label>
    </div>

    <div class="imagen">
      <PokemonImg :pokemonId="id2" :mostrarPokemon="mostrar" />
      <label class="nombre" for="">{{ nombre2 }}</label>
    </div>

    <div class="imagen">
      <PokemonImg :pokemonId="id3" :mostrarPokemon="mostrar" />
      <label class="nombre" for="">{{ nombre3 }}</label>
    </div>
  </div>
  <div v-if="puntaje <= 10 && contador < 5" class="jugar">
    <button class="boton" @:click="obtenerVectorPokemon()">Jugar</button>
  </div>

  <div v-if="puntaje >= 10 && contador <= 5">
    <div>
      <h1 class="victoria">Puntaje: {{ puntaje }}</h1>
      <h1 class="victoria">
        Felicitaciones has ganado un premio de $10.000,00
      </h1>
    </div>
    <button class="boton" @:click="reiniciarJuego()">Nuevo Juego</button>
  </div>

  <div v-if="puntaje < 10 && contador == 5">
    <div>
      <h1 class="derrota">Haz utilizado tus 5 intentos</h1>

      <h1 class="derrota">El juego ha termindo, intentalo nuevamente</h1>
    </div>
    <button class="boton" @:click="reiniciarJuego()">Nuevo Juego</button>
  </div>
</template>

<script>
import PokemonImg from "../components/PokemonImg.vue";
import obtenetFachadaPokemon from "../helpers/clientePokemonApi";

export default {
  data() {
    return {
      id1: 1,
      id2: 1,
      id3: 1,
      mostrar: false,
      nombre1: "XXXXXXXXX",
      nombre2: "XXXXXXXXX",
      nombre3: "XXXXXXXXX",
      contador: 0,
      puntaje: 0,
    };
  },
  components: {
    PokemonImg,
  },
  methods: {
    obtenerNumeroRandomico() {
      //return Math.floor(Math.random() * ( 4- 1) + 1);

      return Math.floor(Math.random() * 4);
    },

    async obtenerVectorPokemon() {
      const vectorPokemons = await obtenetFachadaPokemon();
      const arreglo = vectorPokemons;

      const objeto1 = arreglo[this.obtenerNumeroRandomico()];
      const objeto2 = arreglo[this.obtenerNumeroRandomico()];
      const objeto3 = arreglo[this.obtenerNumeroRandomico()];

      this.nombre1 = objeto1.nombre;
      this.nombre2 = objeto2.nombre;
      this.nombre3 = objeto3.nombre;

      this.id1 = objeto1.id;
      this.id2 = objeto2.id;
      this.id3 = objeto3.id;

      this.mostrar = true;

      this.contador++;

      this.obtenerPuntaje();
    },

 
    obtenerPuntaje() {
      if (
        this.id1 == this.id2 &&
        this.id1 == this.id3 &&
        this.id2 == this.id3
      ) {
        this.puntaje = this.puntaje + 5;
      }else if( this.id1 == this.id2 ||
        this.id1 == this.id3 ||
        this.id2 == this.id3){
            this.puntaje= this.puntaje+2
      }
    },

    reiniciarJuego() {
      this.puntaje = 0;
      this.contador = 0;
      this.mostrar = false;
      (this.nombre1 = "XXXXXXXXX"),
        (this.nombre2 = "XXXXXXXXX"),
        (this.nombre3 = "XXXXXXXXX");
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: center;
}
h1 {
  color: black;
  font-weight: bold;
}

.container,
.imagen {
  margin-left: 35px;
  margin-right: 35px;
}

.container,
label {
  margin-top: 15px;
  margin-bottom: 20px;
}

.victoria {
  color: blue;
}

.derrota {
  color: red;
}

.nombre {
  font-weight: bold;
  margin-bottom: 10px;
}
.boton {
  border: 3px solid black;
  padding: 10px 50px 10px 50px;
}
</style>