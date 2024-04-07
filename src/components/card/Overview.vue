<script setup>
    
</script>

<template>
    <div id="overview">
        <div id="location">Lorton</div>
        <div id="current_tempurature">37°</div>
        <div id="current_status">Mostly Clear</div>
        <div id="highest_and_lowest">
            H:54° L:36°
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

        #current_tempurature {
            font-size: 5em;
        }
    }
</style>