<script>
export default {
    name: 'CityList',

    // Receive the list of cities from the parent component.
    props: ['cities'],

    // Declare the events emitted by this component.
    emits: ['select-city'],

    methods: {
        // Emit the selected city to the parent component.
        selectCity(city){
            this.$emit('select-city', city)
        }
    }
}
</script>

<template>
    <ul>
        <!-- Display each city received through props. -->
        <li 
            v-for="city in cities" 
            :key="city"
            @click="selectCity(city)"
        >
        {{ city }}
        </li>
    </ul>
</template>