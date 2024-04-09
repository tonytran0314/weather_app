<script setup>
    
</script>

<template>
    <div class="bar_container">
        <div class="temp_range">
            <div class="current_temp"></div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    .bar_container {
        width: 100px;
        height: 6px;
        background-color: $labelColor;
        border-radius: $baseDistance;

        .temp_range {
            width: 56%;
            height: 100%;
            // background-image: linear-gradient(to right, #AEC6CF, #AEC6CF, #77DD77, #77DD77, yellow, yellow, orange, orange, red, red);
            background-image: linear-gradient(to right, green, yellow);
            border-radius: $baseDistance;
            margin-left: 32%;

            .current_temp {
                width: 6px;
                height: 100%;
                background-color: white;
                border-radius: 50%;
                border: 1px solid black;
                margin-left: 28%;
            }
        }
    }
    
</style>