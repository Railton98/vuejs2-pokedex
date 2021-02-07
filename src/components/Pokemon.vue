<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure class="image is-square">
          <img :src="currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name | upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content">
          <button
            @click.prevent="changeSprite"
            class="button is-medium is-fullwidth"
          >
            Mudar sprite
          </button>
        </div>
      </div>
    </div>
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

      this.currentImg = this.pokemon.front
    })
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
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
  methods: {
    changeSprite() {
      if (this.isFront) {
        this.isFront = false
        this.currentImg = this.pokemon.back
      } else {
        this.isFront = true
        this.currentImg = this.pokemon.front
      }
    },
  },
}
</script>

<style scoped>
#pokemon {
  margin-top: 1%;
}
</style>