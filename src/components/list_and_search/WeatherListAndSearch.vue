<script setup>
    import ListItem from './ListItem.vue';
    import SearchItem from './SearchItem.vue';

    import axios from 'axios'
    import { ref, watchEffect } from 'vue';

    const search = ref('')
    let searchResults = ref([])
    let searchRecommendDisplay = ref('none')

    const cities = ref([
        {
            'location': 'My Location',
            'time': 'Fairfax',
            'current_temp': '60',
            'weather_status': 'Cloudy',
            'high_temp': '70',
            'low_temp': '50'
        },
        {
            'location': 'Fairfax',
            'time': '3:19 AM',
            'current_temp': '60',
            'weather_status': 'Cloudy',
            'high_temp': '70',
            'low_temp': '50'
        }
    ])

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
                    :country="search.country" />
            </div>
        </div>
        <div id="list_container">
            <ListItem 
                v-for="city in cities"
                :location="city.location"
                :time="city.time"
                :current_temp="city.current_temp"
                :weather_status="city.weather_status"
                :high_temp="city.high_temp"
                :low_temp="city.low_temp" />
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