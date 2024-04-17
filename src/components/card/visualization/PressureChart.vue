<script setup>
    
</script>

<template>
    <div id="pressure_chart_container" class="chart_item">
        <div id="pressure_circle">
            <div id="current_pressure">
                <span>30.06</span>inHg
            </div>
            <div id="current_pressure_mark"></div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #pressure_chart_container {
        width: 100%;
        height: auto;
        // background-color: red;
        display: flex;
        justify-content: center;
        padding: $baseDistance * 2 0 $baseDistance * 3 0;

        #pressure_circle {
            width: $baseDistance * 15;
            height: $baseDistance * 15;
            // background-color: yellow;
            border-radius: 50%;
            border: 2px solid $white;
            border-bottom: 1px solid $mainBackgroundColor;
            position: relative;

            &::before {
                content: 'Low';
                position: absolute;
                bottom: -16px;
            }

            &::after {
                content: 'High';
                position: absolute;
                right: 0;
                bottom: -16px;
            }

            #current_pressure {
                width: $baseDistance * 12;
                height: $baseDistance * 12;
                background-color: $mainBackgroundColor;
                position: absolute;
                border-radius: 50%;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                z-index: 2;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;

                span {
                    font-size: 1.8em;
                }
            }

            #current_pressure_mark {
                width: 2px;
                height: 70px;
                background-color: $white;
                position: absolute;
                left: 50%;
                top: 20%;
                transform: translate(-50%, -50%);
                rotate: 45deg;
                z-index: 1;
            }

        }
    }    
</style>