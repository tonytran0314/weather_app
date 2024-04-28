<script setup>
    const props = defineProps({
        'location': {
            type: String
        },
        'time': {
            type: String
        },
        'current_temp': {
            type: Number
        },
        'weather_status': {
            type: String
        },
        'high_temp': {
            type: Number
        },
        'low_temp': {
            type: Number
        },
    })
</script>

<template>
    <div class="list_item_container">
        <div class="item">
            <div class="top">
                <div class="location">
                    <p>{{ location }}</p>
                    <br />
                    <span>{{ time }}</span>
                </div>
                <div class="current_temp">{{ current_temp }}°</div>
            </div>
            <div class="bottom">
                <div class="weather_status">{{ weather_status }}</div>
                <div class="high_low_temp">H:{{ high_temp }}° L:{{ low_temp }}°</div>
            </div>
        </div>
        <div class="remove">
            <svg width="24px" height="24px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M4 6H20L18.4199 20.2209C18.3074 21.2337 17.4512 22 16.4321 22H7.56786C6.54876 22 5.69264 21.2337 5.5801 20.2209L4 6Z" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M7.34491 3.14716C7.67506 2.44685 8.37973 2 9.15396 2H14.846C15.6203 2 16.3249 2.44685 16.6551 3.14716L18 6H6L7.34491 3.14716Z" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M2 6H22" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M10 11V16" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M14 11V16" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    .list_item_container {
        display: flex;
        justify-content: space-between;
        gap: $baseDistance * 1.5;

        .item {
            background-color: $mainOpacityBackgroundColor;
            padding: $baseDistance * 2;
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: $baseDistance * 4;
            border-radius: $baseDistance * 1.5;
            cursor: pointer;

            .top {
                display: flex;
                justify-content: space-between;

                .location {

                    p {
                        font-size: 1.8em;
                        overflow: hidden;
                        width: $baseDistance * 39;
                        max-width: $baseDistance * 39;
                        height: 34px;
                    }

                    span {
                        display: flex;
                        font-size: 0.8em;
                    }
                }

                .current_temp {
                    font-size: 2.5em;
                }
            }

            .bottom {
                display: flex;
                justify-content: space-between;
            }
        }

        .remove {
            display: flex;
            align-items: center;

            svg {
                cursor: pointer;
            }
        }
    }
    
</style>