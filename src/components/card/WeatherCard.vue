<script setup>
    import axios from 'axios'
    import { ref, reactive, onMounted, provide } from 'vue'

    import Overview from './Overview.vue'
    import Details from './Details.vue'

    // should merge them to 1 object
    const city = ref('Lorton')
    const currentTemp = ref('')
    const condition = ref('')
    const lowestTemp = ref('')
    const highestTemp = ref('')
    const hours = ref([])
    const days = ref([])
    const aqi = ref('')
    const uv = ref('')
    const windMph = ref('')
    const windDegree = ref('')
    const precip = ref('')
    const feelsLike = ref('')
    const humidity = ref('')
    const visibility = ref('')
    const pressure = ref('')
    const isDay = ref('')

    const getForecastURL = "https://api.weatherapi.com/v1/forecast.json?key=00be241cf600489497b10236240604&q="+ city.value +"&days=3&aqi=yes&alerts=no";


    const getForecast = async () => {
        await axios
            .get(getForecastURL)
            .then((res) => {
                currentTemp.value = Math.round(res.data.current.temp_f)
                condition.value = res.data.current.condition.text
                lowestTemp.value = Math.round(res.data.forecast.forecastday[0].day.mintemp_f)
                highestTemp.value = Math.round(res.data.forecast.forecastday[0].day.maxtemp_f)
                hours.value = res.data.forecast.forecastday[0].hour
                days.value = res.data.forecast.forecastday
                aqi.value = res.data.current.air_quality.co
                uv.value = res.data.current.uv
                windMph.value = res.data.current.wind_mph
                windDegree.value = res.data.current.wind_degree
                feelsLike.value = res.data.current.feelslike_f
                precip.value = res.data.current.precip_in
                humidity.value = res.data.current.humidity
                visibility.value = res.data.current.vis_miles
                pressure.value = res.data.current.pressure_in
                isDay.value = res.data.current.is_day
            })
            .catch((error) => console.log(error))
    }

    onMounted(() => {
        getForecast()
    })

    // Overview
    provide('city',         city)
    provide('currentTemp',  currentTemp)
    provide('condition',    condition)
    provide('lowestTemp',   lowestTemp)
    provide('highestTemp',  highestTemp)

    // Detail 
    provide('hours',        hours)          // Hours
    provide('days',         days)           // Days
    provide('aqi',          aqi)            // AQI
    provide('uv',           uv)             // UV
    provide('windMph',      windMph)        // Wind mph
    provide('windDegree',   windDegree)     // Wind degree
    provide('feelsLike',    feelsLike)      // Feels like
    provide('precip',       precip)         // Precipitation
    provide('humidity',     humidity)       // Humidity
    provide('visibility',   visibility)     // Visibility
    provide('pressure',     pressure)       // Pressure
    
    provide('isDay',        isDay)          // Is day
    
</script>

<template>
    <div id="weather_card">
        <Overview />
        <Details />
    </div>
</template>

<style lang="scss" scoped>

    @import '../../assets/variables';

    #weather_card {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>