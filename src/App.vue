<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <input
        class="input is-rounded"
        type="text"
        placeholder="Buscar pokemon pelo nome..."
        v-model="search"
      />
      <button
        id="searchBtn"
        class="button is-fullwidth is-success"
        @click.prevent="find"
      >
        Buscar
      </button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :num="index + 1" :name="poke.name" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
import Pokemon from "./components/Pokemon"

export default {
  name: "App",
  components: {
    Pokemon,
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      search: "",
    }
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results
        this.filteredPokemons = res.data.results
      })
  },
  methods: {
    find() {
      this.filteredPokemons = this.pokemons
      if (this.search == "" || this.search == " ") {
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter((pokemon) =>
          pokemon.name.includes(this.search.toLocaleLowerCase())
        )
      }
    },
  },
}
</script>

<style scoped>
#searchBtn {
  margin-top: 2%;
}
</style>
