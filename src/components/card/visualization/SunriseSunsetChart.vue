<script setup>
</script>

<template>
    <div id="sunrise_sunset_chart_container">
        <div id="circle_overlay">
            <div id="sunrise_sunset_circle"></div>
            <div id="time_overlay_bar">
                <div id="time_value"></div>
            </div>
            <div id="seperater"></div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #sunrise_sunset_chart_container {
        width: 100%;
        height: auto;
        padding: $baseDistance;
        display: flex;
        justify-content: center;
        position: relative;

        #circle_overlay {
            position: relative;

            #sunrise_sunset_circle {
                width: $baseDistance * 15;
                height: $baseDistance * 15;
                border-radius: 50%;
                border-left: 2px solid $white;
                border-top: 2px solid $white;
                border-right: 2px solid $labelColor;
                border-bottom: 2px solid $labelColor;
                rotate: 45deg;
            }

            #time_overlay_bar {
                width: 2px;
                height: 100px;
                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                transform-origin: 0 0;
                rotate: -130deg;

                #time_value {
                    width: 12px;
                    height: 12px;
                    background-color: $white;
                    border-radius: 50%;
                    position: absolute;
                    top: -15px;
                    left: -4px;
                }
            }

            #seperater {
                width: 160px;
                height: 2px;
                background-color: $white;
                position: absolute;
                top: 50%;
                left: -20px;
            }
        }
    }
    
</style>