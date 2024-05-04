<template>
  <div class="weather-search">
    <div class="search-container">
      <input type="text" v-model="query" placeholder="Enter city or location" class="search-input">
      <button @click="searchWeather" class="search-button">Search</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup(props, { emit }) {
    const query = ref('');

    const searchWeather = () => {
      emit('search', query.value);
      query.value = '';
    };

    return { query, searchWeather };
  }
};
</script>

<style scoped>
.weather-search{
  padding-top: 25px;
}
.search-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.search-input {
  width: 100%;
  max-width: 300px;
  padding: 15px;
  border: none;
  outline: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: 0.4s;
}

.search-button {
  padding: 15px 30px;
  margin-left: 10px;
  border: none;
  border-radius: 5px;
  background-color: #4CAF50;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

.search-button:hover {
  background-color: #45a049;
}

@media (max-width: 768px) {
  .search-container {
    flex-direction: column;
  }

  .search-button {
    margin-left: 0;
    margin-top: 10px;
  }
}
</style>
