<template>
  <div class="container">
    <HeaderSection />
    <div class="wrapper">
      <div class="item-wrapper">
        <div v-for="pokemon in pokemons" :key="pokemon.url" class="item">
          <div class="item-img-wrapper">
            <img class="item-img" :src="pokemon.image" :alt="pokemon.name" />
          </div>
          <div class="item-content">
            {{ pokemon.name }}
          </div>
        </div>
      </div>
    </div>
    <FooterSection />
  </div>
</template>

<script>
import { getAllPokemons } from '../api/getAllPokemons'
import HeaderSection from '../components/HeaderSection'
import FooterSection from '../components/FooterSection'

export default {
  components: {
    HeaderSection,
    FooterSection,
  },
  async asyncData() {
    const pokemons = await getAllPokemons()

    return {
      count: pokemons.data.pokemons.count,
      pokemons: pokemons.data.pokemons.results,
    }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
}

.wrapper {
  @apply mt-24 mb-4;
}

.item-wrapper {
  @apply grid grid-cols-1 gap-y-5 mx-4;
}

.item {
  @apply flex items-center rounded-lg overflow-hidden shadow;
}

.item-img-wrapper {
  @apply bg-gray-800;
}

.item-img {
  @apply w-16;
}

.item-content {
  @apply p-4 text-xl;
}
</style>
