<script setup>
    
</script>

<template>
    <div class="detail_item" id="days">
        <div class="title_container">
            <div class="title_icon">icon</div>
            <div class="title">10-DAY FORECAST</div>
        </div>
        <div id="days_forecast">
            <!-- Start loop -->
            <div class="days_forecast_item">
                <div class="date">Today</div>
                <div class="day_weather_status_icon">icon</div>
                <div class="tempurature_range">
                    <div class="day_highest_tempurature">38°</div>
                    <div class="tempurature_bar">bar</div>
                    <div class="day_lowest_tempurature">57°</div>
                </div>
            </div>
            <!-- End loop -->
            
            <div class="days_forecast_item">
                <div class="date">Today</div>
                <div class="day_weather_status_icon">icon</div>
                <div class="tempurature_range">
                    <div class="day_highest_tempurature">38°</div>
                    <div class="tempurature_bar">bar</div>
                    <div class="day_lowest_tempurature">57°</div>
                </div>
            </div>
            
            <div class="days_forecast_item">
                <div class="date">Today</div>
                <div class="day_weather_status_icon">icon</div>
                <div class="tempurature_range">
                    <div class="day_highest_tempurature">38°</div>
                    <div class="tempurature_bar">bar</div>
                    <div class="day_lowest_tempurature">57°</div>
                </div>
            </div>
            
            <div class="days_forecast_item">
                <div class="date">Today</div>
                <div class="day_weather_status_icon">icon</div>
                <div class="tempurature_range">
                    <div class="day_highest_tempurature">38°</div>
                    <div class="tempurature_bar">bar</div>
                    <div class="day_lowest_tempurature">57°</div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

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
</style>