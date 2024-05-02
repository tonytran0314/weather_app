<script setup>
  import OptionsButton from './components/OptionsButton.vue';
  import WeatherCard from './components/card/WeatherCard.vue';
  import WeatherListAndSearch from './components/list_and_search/WeatherListAndSearch.vue';
  
  import { ref, watchEffect } from 'vue'

  const backgroundColor = ref('')
  const showWeatherCard = ref(true)
  const isDay = ref(0)
  
  const currentLocation = ref('Fairfax')
  const location = ref(currentLocation.value)

  const optionButtonClick = () => {
    showWeatherCard.value = !showWeatherCard.value
  }

  const openWeatherItem = (openedWeather) => {
    showWeatherCard.value = true
    location.value = (openedWeather === 'My Location') ? currentLocation.value : openedWeather
  }

  const setIsDay = (isDayValue) => {
    isDay.value = isDayValue
  }
   
  watchEffect(() => {
    backgroundColor.value = 
      (isDay.value === 1 && showWeatherCard.value) ? 
        'rgb(76, 130, 183)' : 
        'rgb(14, 23, 39)'
  })
</script>

<template>

  <div id="option_button" @click="optionButtonClick">
    <OptionsButton />
  </div>

  <div id="weather_container">

    <!-- display this -->
    <WeatherCard 
      v-show="showWeatherCard"
      :location="location"
      @isDay="setIsDay" />

    <!-- or this -->
    <WeatherListAndSearch
      v-show="!showWeatherCard"
      @openedWeather="openWeatherItem" />

  </div>
</template>

<style lang="scss" scoped>

  @import '/src/assets/variables';

  #option_button {
    position: relative;
  }

  #weather_container {
    width: $baseDistance * 60;
    height: 80vh;
    background-color: v-bind(backgroundColor);
    border-radius: $baseDistance * 3;
    color: $white;
    overflow-x: hidden;
    overflow-y: scroll;
    padding: $baseDistance * 2;

    // hide scrollbar for IE and Edge
    -ms-overflow-style: none;

    // hide scrollbar for Firefox
    scrollbar-width: none;

    // hide scrollbar for Chrome, Safari and Opera
    &::-webkit-scrollbar {
      display: none;
    }
  }
</style>