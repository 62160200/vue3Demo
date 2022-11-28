<template>
  <div>
    <h1>PokeAPI</h1>
    <p>
      This is the App page. This page is using the PokeAPI to get the data of the pokemon.
    </p>
    <select name="pokemon" id="pokemon" v-model="selectedPokemon" @change="getPokemon">
      <option value="" disabled>Select a pokemon</option>
      <option
        v-for="pokemon in pokemonList"
        :key="pokemon.name"
        :value="pokemon.url.split('/')[6]"
      >
        No.{{ pokemon.url.split("/")[6] + " " + pokemon.name }}
      </option>
    </select>
  </div>
  <OnDetails :DataPokemon="DataPokemon" v-show="showDetails" />
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import OnDetails from "./components/OnDetails.vue";

const pokemonList: any = ref([]);
const selectedPokemon: any = ref("");
const DataPokemon: any = ref([]);
const showDetails: any = ref(false);

onMounted(async () => {
  const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=151");
  const data = await response.json();
  pokemonList.value = data.results;
});

const getPokemon = () => {
  const response = fetch(`https://pokeapi.co/api/v2/pokemon/${selectedPokemon.value}`);
  response
    .then((res) => res.json())
    .then((data) => {
      DataPokemon.value = data;
    });
  showDetails.value = true;
};
</script>
<style scoped lang="scss">
select {
  text-transform: capitalize;
}
</style>
