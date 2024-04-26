<script setup>
    import { inject } from 'vue'

    const location = inject('location')
    const currentTemp = inject('currentTemp')
    const condition = inject('condition')
    const lowestTemp = inject('lowestTemp')
    const highestTemp = inject('highestTemp')
</script>

<template>
    <div id="overview">
        <div id="location">{{ location }}</div>
        <div id="current_temperature">{{ currentTemp }}°</div>
        <div id="current_status">{{ condition }}</div>
        <div id="highest_and_lowest">
            H:{{ highestTemp }}° L:{{ lowestTemp }}°
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import '../../assets/variables';
    
    #overview {
        padding: $baseDistance*10 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: $baseDistance;

        #location {
            font-size: 1.5em;
        }

        #current_status, #highest_and_lowest {
            font-size: 1.1em;
        }

        #current_temperature {
            font-size: 5em;
        }
    }
</style>