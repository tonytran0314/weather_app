<script setup>
    import { inject, ref, watchEffect } from 'vue';

    const precip = inject('precip')
    const days = inject('days')
    // 3 should be a variable
    const NONE_EXPECTED = "None expected in next 3 days"

    let precipDescription = ref('')

    watchEffect(() => {
        const getNextExpectedPrecip = () => {
            // loops through days
            for(let dayIndex = 0; dayIndex < days.value.length; dayIndex++) {

                // loop through hours of each day
                for(let hourIndex = 0; hourIndex < days.value[dayIndex].hour.length; hourIndex++) {

                    // if precip > 0, get it
                    if(days.value[dayIndex].hour[hourIndex].precip_in > 0) {
                        const precipValue = days.value[dayIndex].hour[hourIndex].precip_in
                        return {
                            "day": getDayFromDate(days.value[dayIndex].date),
                            "value": precipValue
                        }
                    }
                }
            }
            return null;
        }

        const getDayFromDate = (dateInput) => {
            const DAYS = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
            const date = new Date(dateInput)
            return DAYS[date.getDay()]
        }

        const assignDescription = () => {
            if(nextExpectedPrecip == null) {
                return NONE_EXPECTED
            }
            return "Next expected is " + nextExpectedPrecip.value + "'' rain " + nextExpectedPrecip.day
        }

        
        const nextExpectedPrecip = getNextExpectedPrecip()
        precipDescription.value = assignDescription()


    })
</script>

<template>
    <div class="detail_item row_item" id="precipitation">
        <div class="title_container">
            <div class="title_icon">
                <svg fill="rgb(98, 116, 139)" width="16px" height="16px" viewBox="0 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg">
                    <path d="M25.378 19.75c1.507 6.027-3.162 11.25-9.375 11.25s-10.9-5.149-9.375-11.25c0.937-3.75 5.625-9.375 9.375-18.75 3.75 9.374 8.438 15 9.375 18.75z"></path>
                </svg>
            </div>
            <div class="title">PRECIPITATION</div>
        </div>
        <div class="row_item_body">
            <div id="precipitation_overview">
                <div id="precipitation_value">{{ precip }}''</div>
                <div id="precipitation_period">in last 24h</div>
            </div>
            <div id="precipitation_description">{{ precipDescription }}</div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    #precipitation_value {
        font-size: 2.5em;
    }

    #precipitation_period {
        font-size: 1.2em;
    }
    
</style>