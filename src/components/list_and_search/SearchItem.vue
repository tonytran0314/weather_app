<script setup>

    import { ref, reactive, watchEffect } from 'vue';
    import axios from 'axios';

    const emit = defineEmits(['newCity'])
    const props = defineProps({
        'name': {
            type: String
        },
        'region': {
            type: String
        },
        'country': {
            type: String
        }
    })
    
    // separate: url, version, endpoint, search, days, aqi, alerts, *** api_key should be stored in .env file 
    // or all of them store in .env file
    let summary = reactive({
        location: null,
        region: null,
        country: null,
        time: null,
        currentTemp: null,
        weatherStatus: null,
        highTemp: null,
        lowTemp: null,
        isDay: null
    })

    const getWeatherSummary = async (city) => {
    
        const url = 'https://api.weatherapi.com'
        const version = '/v1'
        const endpoint = '/forecast.json'
        const apiKey = '00be241cf600489497b10236240604'
        const forecastdays = 1
        const aqi = 'no'
        const alerts = 'no'
        const getWeatherSummaryURL = 
            url + 
            version + 
            endpoint + 
            "?key=" + apiKey + 
            "&q="+ city + 
            "&days=" + forecastdays + 
            "&aqi=" + aqi + 
            "&alerts=" + alerts;

        await axios
            .get(getWeatherSummaryURL)
            .then((res) => {
                summary.location = res.data.location.name
                summary.region = res.data.location.region
                summary.country = res.data.location.country
                summary.time = getTime(res.data.location.localtime)
                summary.currentTemp = Math.round(res.data.current.temp_f)

                summary.weatherStatus = res.data.current.condition.text
                summary.highTemp = Math.round(res.data.forecast.forecastday[0].day.maxtemp_f)
                summary.lowTemp = Math.round(res.data.forecast.forecastday[0].day.mintemp_f)

                summary.isDay = res.data.current.is_day
            })
            .catch((error) => console.log(error))
    }
        
    const emitNewCity = () => {
        emit('newCity', summary)
    }

    const getTime = (dateTime) => {
        dateTime = new Date(dateTime)
        let suffix = 'AM'
        let hour = dateTime.getHours()
        const minute = dateTime.getMinutes()
        let time = hour + ':' + minute + ' ' + suffix

        // PM if hour >= 12
        if(hour >= 12) {
            hour -= 12
            suffix = 'PM'
        }

        return time
    }

    watchEffect(() => {
        getWeatherSummary(props.name)
    })
    
</script>

<template>
    <div class="search_item" @click="emitNewCity">
        <span v-show="name">{{ name }}</span>
        <span v-show="region">, {{ region }}</span>
        <span v-show="country">, {{ country }}</span>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    .search_item {
        padding: $baseDistance * 2 $baseDistance * 3;
        transition: .2s;

        &:hover {
            background-color: $labelColor;
            border-radius: $baseDistance;
            cursor: pointer;
        }
    }
    
</style>