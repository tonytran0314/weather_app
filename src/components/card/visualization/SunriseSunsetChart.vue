<script setup>
</script>

<template>
    <div id="sunrise_sunset_chart_container">
        <div id="sunrise_sunset_circle"></div>
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
        // background-color: gray;
        position: relative;

        #sunrise_sunset_circle {
            width: $baseDistance * 15;
            height: $baseDistance * 15;
            // background-color: red;
            border-radius: 50%;
            border-left: 4px solid $white;
            border-top: 4px solid $white;
            border-right: 2px solid $labelColor;
            border-bottom: 2px solid $labelColor;
            rotate: 45deg;
        }
    }
    
</style>