<script>
export default {
  name: 'WeatherApp',

  data() {
    return {
      cities : ['Annecy' , 'Paris' , 'Lyon' , 'Grenoble'],
      showCities: true
    }
  }
}
</script>

<template>
  <h1>Ma premiere application meteo</h1>
  
  <button @click = "showCities = !showCities">
  Afficher / masquer les villes
  </button>

  <ul v-if="showCities">
    <li v-for="city in cities" :key="city">
      {{city}}
    </li>
  </ul>

</template>