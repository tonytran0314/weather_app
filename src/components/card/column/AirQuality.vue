<script setup>
    
</script>

<template>
    <div class="detail_item" id="air_quality">
        <div class="title_container">
            <div class="title_icon">icon</div>
            <div class="title">AIR QUALITY</div>
        </div>
        <div id="air_quality_body">
            <div id="air_quality_overview">37 - Good</div>
            <div id="air_quality_description">Air quality index is 37, which is similar to yesterday at about this time</div>
            <div id="air_quality_bar">bar</div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

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
</style>