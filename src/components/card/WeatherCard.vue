<script setup>
    import Overview from './Overview.vue'
    import Details from './Details.vue'

    import axios from 'axios'
    import { ref, provide, watchEffect } from 'vue'

    const props = defineProps({
        location: {
            type: String
        }
    })

    // let forecast = reactive({
    //     location: null,
    //     localTime: null,
    //     currentTemp: null,
    //     condition: null,
    //     lowestTemp: null,
    //     highestTemp: null,
    //     hours: null,
    //     days: null,
    //     isDay: null,
    //     uv: null,
    //     windMph: null,
    //     windDegree: null,
    //     precip: null,
    //     feelsLike: null,
    //     humidity: null,
    //     visibility: null,
    //     pressure: null,
    //     tomorrowHours: null,
    //     astro: null
    // })

    // should merge them to 1 object
    const location = ref('')
    const localTime = ref('')
    const currentTemp = ref('')
    const condition = ref('')
    const lowestTemp = ref('')
    const highestTemp = ref('')
    const hours = ref([])
    const days = ref([])
    const isDay = ref('')
    const uv = ref('')
    const windMph = ref('')
    const windDegree = ref('')
    const precip = ref('')
    const feelsLike = ref('')
    const humidity = ref('')
    const visibility = ref('')
    const pressure = ref('')
    const tomorrowHours = ref([])
    const astro = ref([])

    const emit = defineEmits(['isDay'])
    
    const getForecast = async (locationName) => {

        // separate: url, version, endpoint, search, days, aqi, alerts, *** api_key should be stored in .env file 
        const url = 'https://api.weatherapi.com'
        const version = '/v1'
        const endpoint = '/forecast.json'
        const apiKey = '00be241cf600489497b10236240604'
        const forecastdays = 3
        const aqi = 'no'
        const alerts = 'yes'
        const getForecastURL = 
            url + 
            version + 
            endpoint + 
            "?key=" + apiKey + 
            "&q="+ locationName + 
            "&days=" + forecastdays + 
            "&aqi=" + aqi + 
            "&alerts=" + alerts;

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

                // loop through from today to the next days, add sunrise and sunset time to an array
                // today and tomorrow only
                for(let dayIndex = 0; dayIndex <= 1; dayIndex++) {
                    astro.value.push(new Date(days.value[dayIndex].date + ' ' + days.value[dayIndex].astro.sunrise))
                    astro.value.push(new Date(days.value[dayIndex].date + ' ' + days.value[dayIndex].astro.sunset))
                }
            })
            .catch((error) => console.log(error))
    }

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

    watchEffect(() => {
        getForecast(props.location)
        emit('isDay', isDay.value)
    })
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