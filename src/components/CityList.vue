<script>
export default {
  name: 'CityList',

  // Receive the city list and the selected city from the parent.
  props: ['cities', 'selectedCity'],

  // Declare the event emitted by this component.
  emits: ['select-city'],

  methods: {
    // Send the selected city to the parent.
    selectCity(city) {
      this.$emit('select-city', city)
    }
  }
}
</script>

<template>
  <ul class="city-list">
    <li v-for="city in cities" :key="city">
      <button
        type="button"
        class="city-chip"
        :class="{ 'city-chip--active': city === selectedCity }"
        @click="selectCity(city)"
      >
        {{ city }}
      </button>
    </li>
  </ul>
</template>

<style scoped>
.city-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.65rem;
  margin: 0;
  padding: 0;
  list-style: none;
}

.city-list li {
  margin: 0;
  padding: 0;
}

.city-chip {
  padding: 0.7rem 1rem;
  border: 1px solid #dce6ef;
  border-radius: 999px;
  background: #f6f9fc;
  color: #31566f;
  font: inherit;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s, border-color 0.2s, transform 0.2s;
}

.city-chip:hover {
  border-color: #9fc8e5;
  background: #e6f3fc;
  transform: translateY(-1px);
}

.city-chip--active {
  border-color: #286f9b;
  background: #286f9b;
  color: #fff;
}

.city-chip:focus-visible {
  outline: 3px solid #9fc8e5;
  outline-offset: 3px;
}
</style>