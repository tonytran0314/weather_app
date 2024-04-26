<script setup>
    import SunriseSunsetChart from '../visualization/SunriseSunsetChart.vue';
    import { ref, inject, watchEffect } from 'vue';

    const isDay = inject('isDay')
    const astro = inject('astro')
    const local = inject('localTime')
    const title = ref('')
    let nextSunriseOrSunsetTime = ref('')

    const toStandardDateTime = (string) => {
        return new Date(string)
    }

    watchEffect(() => {
        // title assignment
        title.value = isDay == 1 ? 'Sunset' : 'Sunrise' 

        
        // convert 24-hour time to 12-hour time
        const to12HourTime = (time) => {
            const hour = time[0]
            const minute = time[1]

            if(hour == 0) { return '12:' + minute + 'AM' }
            if(hour == 12) { return '12:' + minute + 'PM' }

            // for AM time
            if(hour > 0 && hour < 12) {
                return hour + ':' + minute + 'AM'
            }

            // for PM time
            if(hour > 12 && hour <=23) {
                return (hour - 12) + ':' + minute + 'AM'
            }
        }

        const localDateTime = toStandardDateTime(local.value)

        const getNextSunriseOrSunsetTime = () => {
            for(let sunIndex = 0; sunIndex < astro.value.length; sunIndex++) {
                astro.value[sunIndex] = toStandardDateTime(astro.value[sunIndex]) // element to standard date time element
                
                let time = []

                if(localDateTime < astro.value[0]) {
                    time = [
                        astro.value[0].getHours(),
                        astro.value[0].getMinutes()
                    ]
                    return to12HourTime(time)
                }

                if (localDateTime > astro.value[sunIndex] && localDateTime < astro.value[sunIndex + 1]) {
                    time = [
                        astro.value[sunIndex + 1].getHours(),
                        astro.value[sunIndex + 1].getMinutes()
                    ]
                    return to12HourTime(time)
                }
            }
        }

        nextSunriseOrSunsetTime = getNextSunriseOrSunsetTime()
    })
</script>

<template> 
    <div class="detail_item row_item" id="sunrise_sunset">
        <div class="title_container">
            <div class="title_icon">

            <!-- Sunset icon -->
            <svg 
                v-if="isDay == 1"
                width="16px" height="16px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M8 18C8 15.7909 9.79086 14 12 14C14.2091 14 16 15.7909 16 18" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="21" y1="21" x2="3" y2="21" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="12" y1="11" x2="12" y2="9" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M12 11L12 3" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M12 11L15 8.5" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M12 11L9 8.5" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="5" y1="18" x2="3" y2="18" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="21" y1="18" x2="19" y2="18" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="19.071" y1="11.3432" x2="17.6568" y2="12.7574" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="5.41421" y1="12" x2="6.82843" y2="13.4142" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            
            <!-- Sunrise icon -->
            <svg
                v-if="isDay == 0"
                width="16px" height="16px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M8 18C8 15.7909 9.79086 14 12 14C14.2091 14 16 15.7909 16 18" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="21" y1="21" x2="3" y2="21" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="12" y1="11" x2="12" y2="9" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M12 3L12 11" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M12 3L9 5.5" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M12 3L15 5.5" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="5" y1="18" x2="3" y2="18" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="21" y1="18" x2="19" y2="18" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="19.071" y1="11.3432" x2="17.6568" y2="12.7574" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <line x1="5.41421" y1="12" x2="6.82843" y2="13.4142" stroke="rgb(98, 116, 139)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>

            </div>
            <div class="title">{{ title.toUpperCase() }}</div>
        </div>
        <div class="row_item_body">
            <SunriseSunsetChart />

            <div id="sunrise_sunset_next">{{ title}}: {{ nextSunriseOrSunsetTime }}</div>
        </div>
    </div>
</template>

<style>
    
</style>