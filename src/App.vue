<template>
  <div id="app">
    <SelectBreed
      :breeds="breeds"
      :onBreedSelection="onBreedSelection"
      />
  <div class="image-grid">
    <img class="image-display" v-for="(image, index) in breedImages" :key="index" :src="image"/>
  </div>
  </div>
</template>

<script>
import { BASE_URL, FETCH_BREEDS} from './constants/ApiConstants';
import SelectBreed from './components/SelectBreed.vue';

export default {
  name: 'App',
  components: {
    SelectBreed,
  },
  data: function() {
    return {
      breeds: [],
      breedImages: [],
    }
  },
  created() {
    fetch(`${BASE_URL}${FETCH_BREEDS}`)
      .then(response => response.json())
      .then(breeds => this.breeds = Object.keys(breeds.message))
  },
  methods: {
    onBreedSelection(breed) {
      fetch(`${BASE_URL}breed/${breed}/images`)
        .then(response => response.json())
        .then(responseImages => this.breedImages = responseImages.message);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.image-grid {
  display: flex;
  flex-wrap: wrap;
  align-content:stretch;
  height: 100%;
  margin-top: 25px;
}

.image-display {
  width: 33%;
  height: 400px;
  object-fit: cover;
}
</style>
