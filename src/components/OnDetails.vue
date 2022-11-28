<template>
  <div class="on-details">
    <hr />
    <div class="card mt-2 me-auto ms-auto text-center" style="width: 18rem">
      <img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${DataPokemon.id}.png`"
        class="card-img-top"
      />
      <div class="card-body">
        <h5 class="card-title">No. {{ DataPokemon.id + " " + DataPokemon.name }}</h5>
        <div class="card-text">
          <div>
            <p>Height: {{ (DataPokemon.height * 0.1).toFixed(2) }} m</p>
            <p>Weight: {{ (DataPokemon.weight * 0.1).toFixed(2) }} kg</p>
          </div>
          <div>
            <p>Ability:</p>
            <div v-for="ability in DataPokemon.abilities" :key="ability.id">
              <p>{{ ability.ability.name }}</p>
            </div>
          </div>
          <div>
            <p>Type:</p>
            <div v-for="type in DataPokemon.types" :key="type.slot">
              <p>{{ type.type.name }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { DataPokemon } = defineProps<{
  DataPokemon: any;
}>();
</script>
<style scoped lang="scss">
h5 {
  text-transform: capitalize;
}
</style>
