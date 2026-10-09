<script>
// Import the child component that displays the city list.
import CityList from '../components/CityList.vue'

import axios from 'axios'

export default {
  name: 'WeatherApp',

  // Register the child component.
  components:{
    CityList
  },

  // Define the reactive data of the parent component.
  data() {
    return {
      cities : ['Annecy' , 'Paris' , 'Lyon' , 'Grenoble'],
      showCities: true,
      newCity: '',
      selectedCity:'',

      // Store weather data and track the request state.
      weather: null,
      isLoading: false,
      error: ''
    }
  },
  
  // Define the methods used by this component.
  methods: {

    // Add a city if the input is not empty.
    addCity() {
      if (this.newCity.trim() !== ''){
        this.cities.push(this.newCity)
        this.newCity = ''
      }
    },

    // Fetch the current weather for the selected city using Axios.
    async selectCity(city) {
      this.selectedCity = city
      this.weather = null
      this.error = ''
      this.isLoading = true

      try {
        // Read the API key from the environment variables.
        const apiKey = import.meta.env.VITE_OPENWEATHER_API_KEY

        if (!apiKey) {
          throw new Error('API Key is missing. Check .env.local.')
        }

        // Send an HTTP GET request using Axios.
        const response = await axios.get(
          'https://api.openweathermap.org/data/2.5/weather',
          {
            params: {
              q: `${city},FR`,
              appid: apiKey,
              units: 'metric',
              lang: 'fr'
            }
          }
        )

        // Store the weather data returned by the API.
        this.weather = response.data

      } catch (error) {
        // Handle HTTP errors returned by the API.
        if (error.response?.status === 404) {
          this.error = 'City not found.'
        } else if (error.response?.status === 401) {
          this.error = 'Invalid API Key or API Key not activated.'
        } else if (error.response) {
          this.error = `Weather API error: ${error.response.status}`
        } else {
          this.error = error.message
        }

      } finally {
        // Stop the loading state after the request finishes.
        this.isLoading = false
      }
    }
  }
}
</script>

<template>
  <h1>Ma premiere application meteo</h1>
  
  <!-- Bind the input value to newCity using v-model. -->
  <input 
    v-model="newCity"
    type="text"
    placeholder="Ajouter une ville"
  >  

  <!-- Disable the button when the input is empty. -->
  <button v-bind:disabled="newCity.trim() === '' "
    @click="addCity">
    Ajouter
  </button>

  <!-- Toggle the visibility of the city list. -->
  <button 
    v-bind:title="showCities ? 'Masquer les villes' : 'Afficher les villes' " 
    @click = "showCities = !showCities"
  >
  Afficher / masquer les villes
  </button>

  <!-- Pass the cities to the child component through props.
       Listen for the select-city event emitted by the child. -->
  <CityList 
  v-if="showCities"
  :cities="cities"
  @select-city="selectCity"
  />

  <!-- Display loading, error, or weather data depending on the request state. -->
  <section v-if="selectedCity">
  <h2>Météo à {{ selectedCity }}</h2>

  <p v-if="isLoading">
    Chargement de la météo...
  </p>

  <p v-else-if="error" role="alert">
    {{ error }}
  </p>

  <div v-else-if="weather">
    <h3>{{ weather.weather[0].description }}</h3>

    <p>
      Température : {{ Math.round(weather.main.temp) }} °C
    </p>

    <p>
      Ressenti : {{ Math.round(weather.main.feels_like) }} °C
    </p>

    <p>
      Humidité : {{ weather.main.humidity }} %
    </p>
  </div>
</section>

</template>