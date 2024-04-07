<script setup>
    import HoursForecast from './column/HoursForecast.vue';
    import DaysForecase from './column/DaysForecast.vue';
    import AirQuality from './column/AirQuality.vue';

    import UvIndex from './row/UvIndex.vue';
    import SunriseSunset from './row/SunriseSunset.vue';
    import Wind from './row/Wind.vue';
    import Precipitation from './row/Precipitation.vue';
    import FeelsLike from './row/FeelsLike.vue';
    import Humidity from './row/Humidity.vue';
    import Visibility from './row/Visibility.vue';
    import Pressure from './row/Pressure.vue';
</script>

<template>
    <div id="details">
        <HoursForecast />
        <DaysForecase />
        <AirQuality />

        <div class="row">
            <UvIndex />
            <SunriseSunset />
        </div>
        <div class="row">
            <Wind />
            <Precipitation />
        </div>
        <div class="row">
            <FeelsLike />
            <Humidity />
        </div>
        <div class="row">
            <Visibility />
            <Pressure />
        </div>
    </div>
</template>

<style lang="scss">

    @import '/src/assets/variables';

    #details {
        width: 100%;
        display: flex;
        flex-direction: column;
        gap: $baseDistance;

        .detail_item {
            border-radius: $baseDistance;
            height: auto;
            background-color: $mainOpacityBackgroundColor;
            padding: $baseDistance * 2;
        }
        
        .title_container {
            display: flex;
            gap: $baseDistance;
            color: $labelColor;

            .title {
                font-size: 0.8em;
            }
        }

        .row {
            display: flex;
            gap: $baseDistance;

            .row_item {
                width: 50%;

                .row_item_body {
                    display: flex;
                    flex-direction: column;
                }
            }
        }

    }

</style>