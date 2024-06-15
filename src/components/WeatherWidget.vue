<template>
  <br>
  <q-card class="weather-widget">
    <q-card-section>
      <h1>Weather Widget</h1>
      <q-form @submit.prevent="updateWeather">
        <q-input
          v-model="city"
          placeholder="Enter city"
          outlined
          dense
          class="q-mb-md"
        />
        <q-btn type="submit" label="Search" color="primary" />
      </q-form>
    </q-card-section>
    <q-card-section v-if="weather">
      <p><strong>Location:</strong> {{ weather.name }}</p>
      <p><strong>Temperature:</strong> {{ weather.main.temp }} °C</p>
      <p><strong>Weather:</strong> {{ weather.weather[0].description }}</p>
    </q-card-section>
    <q-card-section v-else>
      <p>Loading...</p>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  name: 'WeatherWidget',
  data() {
    return {
      weather: null,
      city: '',
      API_KEY: '2766fa1365c6f76bffbb56c65dca0377',
      BASE_URL: 'https://api.openweathermap.org/data/2.5/weather',
      UNITS: 'metric'
    };
  },
  methods: {
    async fetchWeather() {
      if (!this.city) return;
      try {
        const response = await fetch(`${this.BASE_URL}?q=${this.city}&units=${this.UNITS}&appid=${this.API_KEY}`);
        const data = await response.json();
        this.weather = data;
        this.updateBackground(this.weather.main.temp);
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    },
    updateWeather() {
      this.fetchWeather();
    },
    updateBackground(temp) {
      const body = document.body;
      body.classList.remove('cold-weather', 'cool-weather', 'warm-weather', 'hot-weather');

      if (temp <= 0) {
        body.classList.add('cold-weather');
      } else if (temp > 0 && temp <= 20) {
        body.classList.add('cool-weather');
      } else if (temp > 20 && temp <= 30) {
        body.classList.add('warm-weather');
      } else {
        body.classList.add('hot-weather');
      }
    }
  },
  mounted() {
    this.fetchWeather();
  }
};
</script>

<style scoped>
.q-mb-md{
  
  background-color: rgba(255, 255, 255, 0.85);
}

.weather-widget {
  position: relative;
  font-family: Arial, sans-serif;
  border: 1px solid #ccc;
  border-radius: 20px;
  color: white;
  padding: 16px;
  width: 300px;
  margin: 0 auto;
  background-image: url(../assets/berawan.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  opacity: 0.7; 
}

.weather-widget * {
  position: relative;
  z-index: 1; 
}

h1 {
  font-size: 24px;
  text-align: center;
}

form {
  margin-bottom: 16px;
  text-align: center;
}

input {
  padding: 8px;
  margin-right: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
