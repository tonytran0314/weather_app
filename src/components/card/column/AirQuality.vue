<script setup>
    import Bar from "../visualization/Bar.vue";

    import { inject, ref, watchEffect  } from "vue";

    const aqi = inject('aqi')
    const aqiLabel = ref('')

    watchEffect(() => {
        if (aqi.value >= 0 && aqi.value < 51) {
            aqiLabel.value = "Good"
        } 
        if (aqi.value >= 51 && aqi.value < 101) {
            aqiLabel.value = "Moderate"
        } 
        if (aqi.value >= 101 && aqi.value < 201) {
            aqiLabel.value = "Unhealthy"
        } 
        if (aqi.value >= 201 && aqi.value < 301) {
            aqiLabel.value = "Very Unhealthy"
        } 
        if (aqi.value >= 301 ) {
            aqiLabel.value = "Hazardous"
        } 
    })
</script>

<template>
    <div class="detail_item" id="air_quality">
        <div class="title_container">
            <div class="title_icon">
                <svg fill="rgb(98, 116, 139)" width="16px" height="16px" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                    <path d="M2.643 6.357c1.747-1.5 3.127-2.686 6.872-.57 1.799 1.016 3.25 1.4 4.457 1.398 2.115 0 3.486-1.176 4.671-2.193a1.037 1.037 0 0 0 .122-1.439.987.987 0 0 0-1.41-.125c-1.746 1.502-3.127 2.688-6.872.57-4.948-2.793-7.266-.803-9.128.797a1.037 1.037 0 0 0-.121 1.439.986.986 0 0 0 1.409.123zm14.712 2.178c-1.746 1.5-3.127 2.688-6.872.57-4.948-2.795-7.266-.804-9.128.795a1.037 1.037 0 0 0-.121 1.439.986.986 0 0 0 1.409.125c1.747-1.501 3.127-2.687 6.872-.572 1.799 1.018 3.25 1.4 4.457 1.4 2.115 0 3.486-1.176 4.671-2.195a1.035 1.035 0 0 0 .122-1.438.986.986 0 0 0-1.41-.124zm0 5.106c-1.746 1.502-3.127 2.688-6.872.572-4.948-2.795-7.266-.805-9.128.795a1.037 1.037 0 0 0-.121 1.439.985.985 0 0 0 1.409.123c1.747-1.5 3.127-2.685 6.872-.57 1.799 1.016 3.25 1.4 4.457 1.4 2.115 0 3.486-1.178 4.671-2.195a1.037 1.037 0 0 0 .122-1.439.988.988 0 0 0-1.41-.125z"/>
                </svg>
            </div>
            <div class="title">AIR QUALITY</div>
        </div>
        <div id="air_quality_body">
            <div id="air_quality_overview">
                {{ Math.round(aqi) }} - 
                {{ aqiLabel }}
            </div>
            <div id="air_quality_description">Air quality index is {{ Math.round(aqi) }}, which is similar to yesterday at about this time</div>
            <Bar
                type="aqi"
                :value="aqi" />
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    #air_quality {
        display: flex;
        flex-direction: column;
        gap: $baseDistance;

        #air_quality_overview {
            font-size: 2em;
        }

        #air_quality_body {
            display: flex;
            flex-direction: column;
            gap: $baseDistance * 2;
        }
    }
</style>