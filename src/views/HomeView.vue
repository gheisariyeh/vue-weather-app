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
  <main class="weather-page">
    <header class="hero">
      <div class="hero-content">
        <p class="eyebrow">VOTRE MÉTÉO LOCALE</p>
        <h1>La météo, en un clin d'œil</h1>
        <p class="hero-subtitle">
          Découvrez le temps qu'il fait dans vos villes préférées.
        </p>
      </div>

      <div class="hero-symbol" aria-hidden="true">
        🌤️
      </div>
    </header>

    <section class="panel city-panel">
      <div class="section-heading">
        <div>
          <p class="eyebrow">EXPLORER</p>
          <h2>Choisir une ville</h2>
        </div>

        <button
          type="button"
          class="ghost-button"
          @click="showCities = !showCities"
        >
          {{ showCities ? 'Masquer' : 'Afficher' }} la liste
        </button>
      </div>

      <form class="city-form" @submit.prevent="addCity">
        <input
          v-model="newCity"
          class="city-input"
          type="text"
          placeholder="Ajouter une ville..."
          autocomplete="off"
        >

        <button
          type="submit"
          class="primary-button"
          :disabled="newCity.trim() === ''"
        >
          + Ajouter
        </button>
      </form>

      <p class="helper-text">
        Sélectionnez une ville pour consulter sa météo.
      </p>

      <CityList
        v-if="showCities"
        :cities="cities"
        :selected-city="selectedCity"
        @select-city="selectCity"
      />
    </section>

    <section v-if="selectedCity" class="weather-section">
      <div class="section-heading weather-heading">
        <div>
          <p class="eyebrow">CONDITIONS ACTUELLES</p>
          <h2>Météo à {{ selectedCity }}</h2>
        </div>

        <span class="location-badge">
          📍 {{ selectedCity }}
        </span>
      </div>

      <div
        v-if="isLoading"
        class="state-card"
        role="status"
      >
        <span class="loading-spinner"></span>

        <div>
          <strong>Chargement de la météo...</strong>
          <p>Nous récupérons les dernières données.</p>
        </div>
      </div>

      <div
        v-else-if="error"
        class="state-card error-card"
        role="alert"
      >
        <strong>Impossible de charger la météo</strong>
        <p>{{ error }}</p>
      </div>

      <div v-else-if="weather" class="weather-card">
        <div class="weather-main">
          <img
            class="weather-icon"
            :src="`https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`"
            :alt="weather.weather[0].description"
          >

          <div class="weather-summary">
            <p class="weather-description">
              {{ weather.weather[0].description }}
            </p>

            <p class="temperature">
              {{ Math.round(weather.main.temp) }}<span>°C</span>
            </p>
          </div>
        </div>

        <div class="weather-metrics">
          <article class="metric-card">
            <span class="metric-symbol">🌡️</span>
            <p class="metric-label">Température ressentie</p>
            <strong>
              {{ Math.round(weather.main.feels_like) }} °C
            </strong>
          </article>

          <article class="metric-card">
            <span class="metric-symbol">💧</span>
            <p class="metric-label">Humidité</p>
            <strong>{{ weather.main.humidity }} %</strong>
          </article>

          <article class="metric-card">
            <span class="metric-symbol">💨</span>
            <p class="metric-label">Vitesse du vent</p>
            <strong>{{ weather.wind.speed }} m/s</strong>
          </article>

          <article class="metric-card">
            <span class="metric-symbol">☁️</span>
            <p class="metric-label">Couverture nuageuse</p>
            <strong>{{ weather.clouds.all }} %</strong>
          </article>
        </div>
      </div>
    </section>

    <footer v-if="weather" class="source-note">
      Données météo fournies par OpenWeatherMap.
    </footer>
  </main>
</template>

<style scoped>
.weather-page {
  --ink: #183b56;
  --muted: #688196;
  --blue: #286f9b;
  --border: #e0eaf2;

  box-sizing: border-box;
  width: min(100%, 1000px);
  margin: 0 auto;
  padding: 2rem 1.25rem 3rem;
  color: var(--ink);
}

.weather-page *,
.weather-page *::before,
.weather-page *::after {
  box-sizing: border-box;
}

.hero {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
  padding: clamp(1.5rem, 5vw, 3rem);
  margin-bottom: 1.5rem;
  border: 1px solid #dceaf5;
  border-radius: 26px;
  background: linear-gradient(135deg, #deefff, #e9edff);
}

.hero-content {
  max-width: 620px;
}

.eyebrow {
  margin: 0 0 0.55rem;
  color: #507792;
  font-size: 0.72rem;
  font-weight: 800;
  letter-spacing: 0.12em;
}

.hero h1 {
  margin: 0;
  color: var(--ink);
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  line-height: 1.15;
  letter-spacing: -0.04em;
}

.hero-subtitle {
  margin: 0.85rem 0 0;
  color: #54728a;
  line-height: 1.6;
}

.hero-symbol {
  flex-shrink: 0;
  font-size: clamp(3.5rem, 9vw, 6rem);
}

.panel {
  padding: clamp(1.25rem, 4vw, 2rem);
  border: 1px solid var(--border);
  border-radius: 24px;
  background: #fff;
  box-shadow: 0 12px 35px rgb(39 76 110 / 6%);
}

.section-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.section-heading .eyebrow {
  margin-bottom: 0.4rem;
}

.section-heading h2 {
  margin: 0;
  color: var(--ink);
  font-size: 1.4rem;
}

.city-form {
  display: flex;
  align-items: stretch;
  gap: 0.75rem;
}

.city-input {
  flex: 1;
  min-width: 0;
  padding: 0.9rem 1rem;
  border: 1px solid #d7e3ed;
  border-radius: 14px;
  background: #f9fbfd;
  color: var(--ink);
  font: inherit;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.city-input:focus {
  outline: none;
  border-color: #68a5cc;
  box-shadow: 0 0 0 3px rgb(73 147 196 / 15%);
}

.primary-button {
  padding: 0.85rem 1.15rem;
  border: 0;
  border-radius: 14px;
  background: var(--blue);
  color: #fff;
  font: inherit;
  font-weight: 650;
  cursor: pointer;
  transition: background 0.2s, transform 0.2s;
}

.primary-button:hover:not(:disabled) {
  background: #1d587d;
  transform: translateY(-1px);
}

.primary-button:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}

.ghost-button {
  padding: 0.65rem 0.9rem;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: #fff;
  color: var(--blue);
  font: inherit;
  font-weight: 600;
  cursor: pointer;
}

.ghost-button:hover {
  background: #f3f8fc;
}

.helper-text {
  margin: 0.8rem 0 1rem;
  color: var(--muted);
  font-size: 0.88rem;
}

.weather-section {
  margin-top: 1.5rem;
}

.weather-heading {
  margin-bottom: 1rem;
  padding: 0.5rem 0.25rem;
}

.location-badge {
  padding: 0.5rem 0.75rem;
  border-radius: 999px;
  background: #e5f2fc;
  color: #315e7e;
  font-size: 0.85rem;
  font-weight: 650;
}

.weather-card {
  padding: clamp(1.25rem, 4vw, 2rem);
  border: 1px solid #e0ebf4;
  border-radius: 24px;
  background: linear-gradient(145deg, #fff, #f0f7fd);
  box-shadow: 0 12px 35px rgb(39 76 110 / 6%);
}

.weather-main {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding-bottom: 1.25rem;
}

.weather-icon {
  width: clamp(90px, 15vw, 130px);
  height: clamp(90px, 15vw, 130px);
  object-fit: contain;
}

.weather-summary {
  min-width: 0;
}

.weather-description {
  margin: 0 0 0.2rem;
  color: #54728a;
  font-size: 1rem;
  text-transform: capitalize;
}

.temperature {
  margin: 0;
  color: var(--ink);
  font-size: clamp(3rem, 8vw, 4.6rem);
  font-weight: 800;
  letter-spacing: -0.06em;
  line-height: 1.1;
}

.temperature span {
  margin-left: 0.2rem;
  font-size: 1.4rem;
  font-weight: 550;
  vertical-align: top;
  letter-spacing: 0;
}

.weather-metrics {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.metric-card {
  padding: 1.1rem;
  border: 1px solid #e3edf5;
  border-radius: 18px;
  background: #fff;
}

.metric-symbol {
  font-size: 1.4rem;
}

.metric-label {
  margin: 0.55rem 0 0.3rem;
  color: var(--muted);
  font-size: 0.85rem;
}

.metric-card strong {
  color: var(--ink);
  font-size: 1.35rem;
}

.state-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.25rem;
  border: 1px solid #dceaf5;
  border-radius: 18px;
  background: #fff;
}

.state-card strong {
  color: var(--ink);
}

.state-card p {
  margin: 0.35rem 0 0;
  color: var(--muted);
  line-height: 1.5;
}

.error-card {
  border-color: #f1cccc;
  background: #fff7f7;
}

.loading-spinner {
  width: 26px;
  height: 26px;
  flex-shrink: 0;
  border: 3px solid #d9eaf7;
  border-top-color: var(--blue);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

.source-note {
  margin-top: 1.25rem;
  color: var(--muted);
  font-size: 0.78rem;
  text-align: center;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

@media (max-width: 600px) {
  .weather-page {
    padding: 1rem 0.85rem 2rem;
  }

  .hero {
    padding: 1.5rem;
    border-radius: 21px;
  }

  .hero-symbol {
    font-size: 3rem;
  }

  .city-form {
    flex-direction: column;
  }

  .primary-button {
    width: 100%;
  }

  .weather-metrics {
    grid-template-columns: 1fr;
  }
}
</style>