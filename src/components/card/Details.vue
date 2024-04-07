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

    @import '../../assets/variables';

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

        #hours {
            display: flex;
            justify-content: space-between;
            gap: $baseDistance * 2;

            #left_arrow, #right_arrow{
                display: flex;
                align-items: center;
                cursor: pointer;
                // background-color: red;
            }

            #hour_slides {
                display: flex;
                align-items: center;
                gap: $baseDistance * 4;
                overflow: hidden;
                width: 100%;
                // background-color: red;

                .hour_item {
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    gap: $baseDistance;
                }
            }
            
        }

        #days {
            display: flex;
            flex-direction: column;
            gap: $baseDistance;

            #days_forecast {
                display: flex;
                flex-direction: column;
                gap: $baseDistance;

                .days_forecast_item {
                    display: flex;
                    justify-content: space-between;
                    border-top: 1px solid $labelColor;
                    padding: $baseDistance*1.5 0 $baseDistance 0;

                    .tempurature_range {
                        display: flex;
                    }
                }
            }
        }

        #air_quality {
            display: flex;
            flex-direction: column;
            gap: $baseDistance;

            #air_quality_overview {
                font-size: 1.3em;
            }

            #air_quality_body {
                display: flex;
                flex-direction: column;
                gap: $baseDistance * 2;
            }
        }

        
        .title_container {
            display: flex;
            gap: $baseDistance;
            color: $labelColor;

            .title {
                font-size: 0.8em;
            }
        }

        // ========================================================== //
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