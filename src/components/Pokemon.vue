<template>
  <div>
    <h1>{{ num }} - {{ name | upper }}</h1>
    <small>{{ url }}</small>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: "Pokemon",
  created() {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name
      this.pokemon.front = res.data.sprites.front_default
      this.pokemon.back = res.data.sprites.back_default
      console.log(this.pokemon)
    })
  },
  data() {
    return {
      pokemon: {},
    }
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: (value) => `${value[0].toUpperCase()}${value.slice(1)}`,
  },
}
</script>

<style>
</style>