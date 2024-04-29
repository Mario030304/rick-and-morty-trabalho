<script setup>
import { onMounted, reactive, ref } from 'vue';

let characters = reactive(ref());

onMounted(() => {
  fetch("https://rickandmortyapi.com/api/character")
  .then(response => response.json())
  .then(response => {
    characters.value = response.results;
    console.log(characters);
  })
  .catch(error => {
    console.error('Error fetching characters:', error);
  });
});

</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6" v-for="character in characters" :key="character.id">
          <div class="card" style="width: 25rem;">
            <img :src="character.image" class="card-img-top" :alt="character.name">
            <div class="card-body">
              <h5 class="card-title">{{ character.name }}</h5>
              <p class="card-text"><strong>Status:</strong> {{ character.status }}</p>
              <p class="card-text"><strong>Espécie:</strong> {{ character.species }}</p>
              <p class="card-text"><strong>Genêro:</strong> {{ character.gender }}</p>
              <p class="card-text"><strong>Localização:</strong> {{ character.location.name }}</p>
              <p class="card-text"><strong>episódios:</strong> {{ character.episode.length }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>