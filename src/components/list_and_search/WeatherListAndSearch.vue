<script setup>
    import ListItem from './ListItem.vue';
    import SearchItem from './SearchItem.vue';

    import axios from 'axios'
    import { ref, watchEffect } from 'vue';

    const search = ref('')
    let searchResults = ref([])
    let searchRecommendDisplay = ref('none')

    const myLocation = ref({
        'location': 'My Location',
        'region': 'Virginia',
        'country': 'The US',
        'time': 'Fairfax',
        'weatherStatus': 'Cloudy',
        'currentTemp': 60,
        'highTemp': 70,
        'lowTemp': 50,
        'isDay': 0
    })

    // [1/2] empty localStorage.cities:
    // const cities = ref([])

    const cities = ref(JSON.parse(localStorage.cities))

    const addNewCity = (summary) => {
        if(newCityValidation(summary)) {
            hideSearchRecommend()
        
            // [2/2] empty localStorage.cities:
            // localStorage.cities = JSON.stringify([])

            // add new city
            cities.value.push(summary)

            // save to localstorage 
            localStorage.cities = JSON.stringify(cities.value)
        }
    }

    const newCityValidation = (newCity) => {

        for(let index = 0; index < cities.value.length; index++) {
            if(
                newCity.location === cities.value[index].location && // same location and
                newCity.region === cities.value[index].region && // same region and
                newCity.country === cities.value[index].country // same country
            ) {
                return false
            }
        } 

        return true
    }

    const hideSearchRecommend = () => {
        searchRecommendDisplay.value = 'none'
    }

    const removeWeatherItem = (removedIndex) => {
        // remove 1 weather item
        cities.value.splice(removedIndex, 1)

        // save to localstorage 
        localStorage.cities = JSON.stringify(cities.value)
    }


    // separate: url, version, endpoint, search, days, aqi, alerts, *** api_key should be stored in .env file 
    // or all of them store in .env file
    const url = 'https://api.weatherapi.com'
    const version = '/v1'
    const endpoint = '/search.json'
    const apiKey = '00be241cf600489497b10236240604'
    
    watchEffect(() => {
        const getSearchResultURL = 
            url + 
            version + 
            endpoint + 
            "?key=" + apiKey + 
            "&q="+ search.value
            
        const getSearchResult = async () => {
            await axios
                .get(getSearchResultURL)
                .then((res) => {
                    searchResults.value = res.data
                })
                .catch((error) => console.log(error))
        }

        if(search.value === '') {
            searchRecommendDisplay.value = 'none'
        } else {
            searchRecommendDisplay.value = 'block'
            getSearchResult()
        }
    })
</script>

<template>
    <div id="weather_list_and_search">
        <div id="search_container">
            <div id="search_bar">
                <input v-model="search" type="text" placeholder="Search for a city or airport">
            </div>
            <div id="search_recommend">
                <SearchItem 
                    v-for="search in searchResults" 
                    :name="search.name"
                    :region="search.region"
                    :country="search.country"
                    @newCity="addNewCity" />
            </div>
        </div>
        <div id="list_container">
            <ListItem 
                :location="myLocation.location"
                :time="myLocation.time"
                :current_temp="myLocation.currentTemp"
                :weather_status="myLocation.weatherStatus"
                :high_temp="myLocation.highTemp"
                :low_temp="myLocation.lowTemp"
                :removable="false" />
            <ListItem 
                v-for="(city, index) in cities"
                :location="city.location"
                :time="city.time"
                :current_temp="city.currentTemp"
                :weather_status="city.weatherStatus"
                :high_temp="city.highTemp"
                :low_temp="city.lowTemp"
                :removable="true"
                :index="index"
                @removedIndex="removeWeatherItem" />
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    #weather_list_and_search {
        margin-top: $baseDistance * 5;
        display: flex;
        flex-direction: column;
        gap: $baseDistance * 5;

        #search_container {
            display: flex;
            justify-content: space-between;
            gap: $baseDistance * 2;
            position: relative;

            #search_bar {
                width: 100%;

                input {
                    padding: $baseDistance*1.5 $baseDistance*3;
                    border-radius: $baseDistance * 3;
                    width: 100%;
                    border: none;
                    background-color: $mainOpacityBackgroundColor;
                    color: $white;

                    &::placeholder {
                        color: $labelColor;
                    }

                    &:focus {
                        outline: none;
                    }
                }
            }

            #search_recommend {
                width: 100%;
                height: auto;
                background-color: black;
                position: absolute;
                left: 0;
                top: $baseDistance * 5.5;
                border-radius: $baseDistance;
                display: v-bind(searchRecommendDisplay);
            }

        }

        #list_container {
            display: flex;
            flex-direction: column;
            gap: $baseDistance * 2;
        }
    }
</style>