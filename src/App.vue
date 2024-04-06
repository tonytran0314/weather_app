<script setup>
  import OptionsButton from './components/OptionsButton.vue';
  import WeatherCard from './components/card/WeatherCard.vue';
  import WeatherListAndSearch from './components/list_and_search/WeatherListAndSearch.vue';
</script>

<template>
  <div id="weather_container">
    
    <OptionsButton />

    <!-- display this -->
    <WeatherCard />
    <!-- or this -->
    <!-- <WeatherListAndSearch /> -->

  </div>
</template>

<style lang="scss" scoped>

  @import './assets/variables';

  #weather_container {
    width: $baseDistance * 60;
    height: 80vh;
    background-color: $cardContainerBackgroundColor;
    border-radius: $baseDistance * 3;
    position: relative;
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