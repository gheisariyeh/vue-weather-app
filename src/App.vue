<script>
export default {
  name: 'WeatherApp',

  data() {
    return {
      cities : ['Annecy' , 'Paris' , 'Lyon' , 'Grenoble'],
      showCities: true,
      newCity: ''
    }
  },
  
  methods: {
    addCity() {
      if (this.newCity.trim() !== ''){
        this.cities.push(this.newCity)
        this.newCity = ''
      }
    }
  }
}
</script>

<template>
  <h1>Ma premiere application meteo</h1>
  
  <input 
    v-model="newCity"
    type="text"
    placeholder="Ajouter une ville"
  >  

  <button v-bind:disabled="newCity.trim() === '' "
    @click="addCity">
    Ajouter
  </button>

  <button 
    v-bind:title="showCities ? 'Masquer les villes' : 'Afficher les villes' " 
    @click = "showCities = !showCities"
  >
  Afficher / masquer les villes
  </button>

  <ul v-if="showCities">
    <li v-for="city in cities" :key="city">
      {{city}}
    </li>
  </ul>

</template>