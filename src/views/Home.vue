<template>
  <div class="flex w-full justify-center">
    <input
      type="text"
      placeholder="Enter pokemon here"
      class="mt-10 p-2 border-blue-500 border-2"
      v-model="state.text"
    />
  </div>
  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div
      class="ml-4 text-2xl text-blue-500"
      v-for="(pokemon, idx) in state.filteredPokemon"
      :key="idx"
    >
      <router-link :to="`/about/${state.urlIdLookup[pokemon.name]}`">
        {{ pokemon.name }}
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { computed, reactive, toRefs } from "vue";

const state = reactive({
  pokemons: [],
  urlIdLookup: {},
  text: "",
  filteredPokemon: computed(() => updatePokemon()),
});

function updatePokemon() {
  if (!state.text) return [];

  return state.pokemons.filter((pokemon) => pokemon.name.includes(state.text));
}

fetch("https://pokeapi.co/api/v2/pokemon?offset=0")
  .then((res) => res.json())
  .then((data) => {
    state.pokemons = data.results;
    state.urlIdLookup = data.results.reduce(
      (acc, cur, idx) => (acc = { ...acc, [cur.name]: idx + 1 }),
      {}
    );
  });
</script>

<style lang="scss" scoped></style>
