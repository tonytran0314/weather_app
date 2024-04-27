<script setup>
  import OptionsButton from './components/OptionsButton.vue';
  import WeatherCard from './components/card/WeatherCard.vue';
  import WeatherListAndSearch from './components/list_and_search/WeatherListAndSearch.vue';

  import axios from 'axios'
  import { ref, onMounted, provide } from 'vue'


  /* -------------------------------------------------------------------------- */
  /*                                WEATHER CARD                                */
  /* -------------------------------------------------------------------------- */


  // should merge them to 1 object
  const location = ref('')
  const localTime = ref('')
  const currentTemp = ref('')
  const condition = ref('')
  const lowestTemp = ref('')
  const highestTemp = ref('')
  const hours = ref([])
  const days = ref([])
  const uv = ref('')
  const windMph = ref('')
  const windDegree = ref('')
  const precip = ref('')
  const feelsLike = ref('')
  const humidity = ref('')
  const visibility = ref('')
  const pressure = ref('')
  const isDay = ref('')
  const tomorrowHours = ref([])
  const astro = ref([])

  const backgroundColor = ref('')

  // separate: url, version, endpoint, search, days, aqi, alerts, *** api_key should be stored in .env file 
  const url = 'https://api.weatherapi.com'
  const version = '/v1'
  const endpoint = '/forecast.json'
  const apiKey = '00be241cf600489497b10236240604'
  const search = ref('Tan Son Nhat International Airport')
  const forecastdays = 3
  const aqi = 'no'
  const alerts = 'yes'
  const getForecastURL = 
    url + 
    version + 
    endpoint + 
    "?key=" + apiKey + 
    "&q="+ search.value + 
    "&days=" + forecastdays + 
    "&aqi=" + aqi + 
    "&alerts=" + alerts;


  const getForecast = async () => {
      await axios
          .get(getForecastURL)
          .then((res) => {
              location.value = res.data.location.name
              localTime.value = res.data.location.localtime
              currentTemp.value = Math.round(res.data.current.temp_f)
              condition.value = res.data.current.condition.text
              lowestTemp.value = Math.round(res.data.forecast.forecastday[0].day.mintemp_f)
              highestTemp.value = Math.round(res.data.forecast.forecastday[0].day.maxtemp_f)
              hours.value = res.data.forecast.forecastday[0].hour
              days.value = res.data.forecast.forecastday
              uv.value = res.data.current.uv
              windMph.value = res.data.current.wind_mph
              windDegree.value = res.data.current.wind_degree
              feelsLike.value = res.data.current.feelslike_f
              precip.value = res.data.current.precip_in
              humidity.value = res.data.current.humidity
              visibility.value = res.data.current.vis_miles
              pressure.value = res.data.current.pressure_in
              isDay.value = res.data.current.is_day
              tomorrowHours.value = res.data.forecast.forecastday[1].hour
              
              backgroundColor.value = isDay.value == 1 ? 'rgb(76, 130, 183)' : 'rgb(14, 23, 39)'

              // loop through from today to the next days, add sunrise and sunset time to an array
              // today and tomorrow only
              for(let dayIndex = 0; dayIndex <= 1; dayIndex++) {
                astro.value.push(new Date(days.value[dayIndex].date + ' ' + days.value[dayIndex].astro.sunrise))
                astro.value.push(new Date(days.value[dayIndex].date + ' ' + days.value[dayIndex].astro.sunset))
              }
          })
          .catch((error) => console.log(error))
  }

  onMounted(() => {
    getForecast()
  })

  // Overview
  provide('location',         location)
  provide('currentTemp',      currentTemp)
  provide('condition',        condition)
  provide('lowestTemp',       lowestTemp)
  provide('highestTemp',      highestTemp)

  // Detail 
  provide('hours',            hours)          // Hours
  provide('days',             days)           // Days
  provide('uv',               uv)             // UV
  provide('windMph',          windMph)        // Wind mph
  provide('windDegree',       windDegree)     // Wind degree
  provide('feelsLike',        feelsLike)      // Feels like
  provide('precip',           precip)         // Precipitation
  provide('humidity',         humidity)       // Humidity
  provide('visibility',       visibility)     // Visibility
  provide('pressure',         pressure)       // Pressure
  
  provide('isDay',            isDay)          // Is day
  provide('tomorrowHours',    tomorrowHours)  // Tomorrow hours
  provide('localTime',        localTime)      // Local time
  provide('astro',            astro)          // Astro
  

  /* -------------------------------------------------------------------------- */
  /*                                OPTION BUTTON                               */
  /* -------------------------------------------------------------------------- */

  const showWeatherCard = ref(true)
  const optionButtonClick = () => {
    showWeatherCard.value = !showWeatherCard.value
  }
</script>

<template>

  <div id="option_button" @click="optionButtonClick">
    <OptionsButton />
  </div>

  <div id="weather_container">

    <!-- display this -->
    <WeatherCard v-show="showWeatherCard" />

    <!-- or this -->
    <WeatherListAndSearch v-show="!showWeatherCard" />

  </div>
</template>

<style lang="scss" scoped>

  @import './assets/variables';

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