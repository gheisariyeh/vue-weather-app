<script>
// Import the child component that displays the city list.
import CityList from '../components/CityList.vue'

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
      selectedCity:''
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

    // Store the city received from the child component.
    selectCity(city) {
      this.selectedCity = city
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

  <!-- Display the selected city after a click. -->
  <p v-if="selectedCity">
    Ville sélectionnée : {{ selectedCity}}
  </p>

</template>