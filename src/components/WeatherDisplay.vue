<template>
  <div class="weather-display" v-if="weather">
    <h2>{{ weather.name }}</h2>
    <h3>{{ displayTemperature }}</h3>
    <p>{{ weather.weather[0].description }}</p>
    <p>Humidity: {{ weather.main.humidity }}%</p>
    <p>Wind Speed: {{ weather.wind.speed }} m/s</p>
    <p>Pressure: {{ weather.main.pressure }} hPa</p>
    <img :src="'http://openweathermap.org/img/wn/' + weather.weather[0].icon + '.png'" :alt="weather.weather[0].description">
    <button class="toggle-button" @click="toggleTemperatureUnits">
      <span class="celsius" :class="{ active: isCelsius }">°C</span>
      <span class="fahrenheit" :class="{ active: !isCelsius }">°F</span>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    weather: Object
  },
  data() {
    return {
      isCelsius: true
    };
  },
  computed: {
    displayTemperature() {
      return this.isCelsius ? `${this.weather.main.temp}°C` : `${(this.weather.main.temp * 9 / 5 + 32).toFixed(1)}°F`;
    }
  },
  methods: {
    toggleTemperatureUnits() {
      this.isCelsius = !this.isCelsius;
    }
  }
};
</script>

<style scoped>
.weather-display {
  text-align: center;
  background: rgb(11, 53, 11);
  opacity: 0.5;
  color: #fff;
  z-index: 1;
  margin: 0 auto;
  max-width: 400px;
}

.weather-display h3, .weather-display p {
  margin: 5px 0;
}

.weather-display img {
  margin-top: 10px;
}

.toggle-button {
  background-color: transparent;
  border-radius: 10px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.toggle-button span {
  padding: 5px 10px;
  transition: all 0.3s ease;
}

.toggle-button .celsius.active {
  color: #ffffff;
  background-color: #4CAF50;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
}

.toggle-button .fahrenheit.active {
  color: #ffffff;
  background-color: #ff9800;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
}

@media (max-width: 768px) {
  .weather-display {
    max-width: 100%;
    margin: 0 20px;
  }
}
</style>
