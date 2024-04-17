<script setup>
</script>

<template>
    <div id="sunrise_sunset_chart">
        <div class="dot"></div>
        <svg height="110px">
            <circle cx="50" cy="50" r="50" id="night_section"></circle>
            <circle cx="50" cy="50" r="50" id="day_section"></circle>
        </svg>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #sunrise_sunset_chart {
        // background-color: gray;
        position: relative;
        

        .dot {
            width: 12px;
            height: 12px;
            background-color: $white;
            border-radius: 50%;
            position: absolute;
            // box-shadow: 0 0 20px $white, 0 0 60px $white;
            transform: rotate(160deg);
            left: 20px;
            border-top-color: red;
        }

        svg { 
            circle {
                fill: transparent;
                stroke-width: 5;
                transform: translate(50px, 5px);
            }

            #day_section {
                stroke: $labelColor;
                stroke-dasharray: 160;
            }
            #night_section {
                stroke: $white;
            }
        }
    }
    
</style>