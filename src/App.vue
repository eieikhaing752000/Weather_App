<template>
  <div id="app">
    <WeatherSearch @search="handleSearch"/>
    <WeatherDisplay v-if="weatherData" :weather="weatherData" />
    <ErrorDisplay v-if="errorMessage" :error="errorMessage" />
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';
import WeatherSearch from './components/WeatherSearch.vue';
import WeatherDisplay from './components/WeatherDisplay.vue';
import ErrorDisplay from './components/ErrorDisplay.vue';

export default {
  name: 'App',
  components: {
    WeatherSearch,
    WeatherDisplay,
    ErrorDisplay
  },
  setup() {
    const weatherData = ref(null);
    const errorMessage = ref(null);

    const handleSearch = async (query) => {
      try {
        const apiKey = 'f608e6418b165f50da448b806305964e';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${query}&appid=${apiKey}&units=metric`;
        const response = await axios.get(apiUrl);
        
        weatherData.value = response.data;
        errorMessage.value = null;
      } catch (error) {
        weatherData.value = null;
        errorMessage.value = 'Failed to fetch weather data. Please try again later.';
      }
    };

    return { weatherData, errorMessage, handleSearch };
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-image: url('assets/bg-image.jpg');
  background-size: cover;
}
</style>
