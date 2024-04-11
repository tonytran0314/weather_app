<script setup>

    import { computed } from 'vue'

    const aqiGradient = 'linear-gradient(to right, green, yellow, orange, red, purple, maroon)'
    const uviGradient = 'linear-gradient(to right, green, yellow, orange, red, purple)'

    const props = defineProps({
        type: {
            type: String
        },
        value: {
            type: Number,
            required: true
        }
    })

    const gradient = computed(() => {
        return props.type == 'aqi' ? aqiGradient : uviGradient
    })

    const marginLeft = computed(() => {
        const UV_HIGH = 11;
        const AQI_HIGH = 301;
        const VALUE_CIRLE_WIDTH = 8; //px

        const highValue = props.type == 'aqi' ? AQI_HIGH : UV_HIGH

        if(props.value >= highValue) {
            return 'calc(100% - ' + VALUE_CIRLE_WIDTH + 'px)'
        }
        
        return (props.value * 100 / highValue) + '%'
    })
</script>

<template>
    <div class="bar_container">
        <div class="current_value"></div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    .bar_container {
        background-image: v-bind(gradient); // param

        width: 100%;
        height: $baseDistance;
        border-radius: $baseDistance;

        .current_value {
            margin-left: v-bind(marginLeft); // param

            width: $baseDistance;
            height: 100%;
            background-color: $white;
            border-radius: 50%;
            border: 1px solid black;
        }
    }
    
</style>