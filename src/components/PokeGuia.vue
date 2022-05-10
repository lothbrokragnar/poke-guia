<template>
  <div>
    <form @submit.prevent="pokemonUrl">
      <label>Nombre: </label>
      <input type="text" placeholder="Escribe tu Pokemón" v-model="newSearch">
      <button type="submit">Buscar</button>
    </form>
    <div class="summary--container">
      <div class="image--container">
        <img class="image--container__image" :src="sprite" alt="">
        <h2 class="image--container__name">{{newSearch}}</h2>
      </div>
      <div class="moves--container">
        <h2>Movimientos</h2>
        <p v-for="(move, i) in moves" :key="i">{{move.move.name}}</p>
      </div>
      <div class="abilities--container">
        <h2>Habilidades</h2>
        <p v-for="(ability, i) in abilities" :key="i">{{ability.ability.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        newSearch: 'pikachu',
        pokemonSearched: [],
      }
    },
    created() {
        this.pokemonUrl()
    },
    methods: {
      pokemonUrl(){
        fetch(`https://pokeapi.co/api/v2/pokemon/${this.newSearch}`)
          .then(response => response.json())
          .then(pokemonInformation => this.pokemonSearched = pokemonInformation);
      }
    },
    computed:{
      moves(){
        return this.pokemonSearched.moves
      },
      abilities(){
        return this.pokemonSearched.abilities
      },
      sprite(){
        return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${this.pokemonSearched.id}.png`
      }
    }
  }
</script>


<style scoped>
.image--container__image{
  width: 200px
}
.image--container__name{
  text-transform: uppercase;
  margin-top: 0;
}

</style>