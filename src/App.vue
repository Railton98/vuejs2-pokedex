<template>
  <div id="app">
    <div v-for="(poke, index) in pokemons" :key="index">
      <Pokemon :num="index + 1" :name="poke.name" :url="poke.url" />
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
    }
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => (this.pokemons = res.data.results))
  },
}
</script>

<style>
</style>
