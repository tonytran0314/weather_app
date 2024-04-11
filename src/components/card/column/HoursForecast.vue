<script setup>

    import { ref, computed } from 'vue'

    const positionNumber = ref(0)
    const slideDistance = 50
    const slidePosition = computed(() => {
        return positionNumber.value + 'px'
    })

    console.log(positionNumber.value)
    const leftArrowClick = computed(() => {
        positionNumber.value += slideDistance
    console.log(positionNumber.value)
    })

    const rightArrowClick = () => {
        positionNumber.value -= slideDistance
    console.log(positionNumber.value)
    }
</script>

<template>
    <div class="detail_item" id="hours">
            <div id="left_arrow" @click="leftArrowClick">
                <svg 
                    width="32px" height="32px" 
                    viewBox="0 0 24 24" 
                    fill="none" 
                    xmlns="http://www.w3.org/2000/svg">
                        <path 
                            d="M15 7L10 12L15 17" 
                            stroke="#FFFFFF" 
                            stroke-width="1.5" 
                            stroke-linecap="round" 
                            stroke-linejoin="round"/>
                </svg>
            </div>
            <div id="hour_slides_container">
                <div id="hour_slides">
                    <!-- Start loop -->
                    <div class="hour_item">
                        <div class="time">Now</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" />
                        </div>
                        <div class="temperature">37°</div>
                    </div>
                    <!-- End loop -->

                    <div class="hour_item">
                        <div class="time">6AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">36°</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">6:45AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">Sunrise</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">7AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">36°</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">8AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">38°</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">6AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">36°</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">6:45AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">Sunrise</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">7AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">36°</div>
                    </div>
                    <div class="hour_item">
                        <div class="time">8AM</div>
                        <div class="icon">
                            <img src="/src/assets/images/clear.png" /></div>
                        <div class="temperature">38°</div>
                    </div>
                </div>
            </div>
            <div id="right_arrow" @click="rightArrowClick">
                <svg 
                    width="32px" height="32px" 
                    viewBox="0 0 24 24" 
                    fill="none" 
                    xmlns="http://www.w3.org/2000/svg">
                        <path 
                            d="M10 7L15 12L10 17" 
                            stroke="#FFFFFF" 
                            stroke-width="1.5" 
                            stroke-linecap="round" 
                            stroke-linejoin="round"/>
                </svg>
            </div>
        </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    #hours {
        display: flex;
        justify-content: space-between;
        gap: $baseDistance * 2;

        #left_arrow, #right_arrow{
            display: flex;
            align-items: center;
            cursor: pointer;
        }

        #hour_slides_container {
            overflow: hidden;
            width: 100%;
            height: 100px;
            position: relative;
            background-color: red;
            scroll-snap-type: x mandatory;

            #hour_slides {
                display: flex;
                gap: $baseDistance * 4;
                align-items: center;
                position: absolute;
                left: 0;
                transform: translateX(v-bind(slidePosition));
                transition: .3s ease;
                background-color: green;

                .hour_item {
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    gap: $baseDistance;

                    .icon {
                        img {
                            width: $baseDistance * 4;
                        }
                    }
                }
            }
        }
        
    }
</style>