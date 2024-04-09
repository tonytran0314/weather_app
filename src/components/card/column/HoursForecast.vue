<script setup>
    
</script>

<template>
    <div class="detail_item" id="hours">
            <div id="left_arrow">
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
            <div id="hour_slides">
            <!-- CHECK CLASS OR ID -->
                <!-- Start loop -->
                <div class="hour_item">
                    <div id="time">Now</div>
                    <div id="icon">
                        <img src="/src/assets/images/clear.png" />
                    </div>
                    <div id="temperature">37°</div>
                </div>
                <!-- End loop -->

                <div class="hour_item">
                    <div id="time">6AM</div>
                    <div id="icon">
                        <img src="/src/assets/images/clear.png" /></div>
                    <div id="temperature">36°</div>
                </div>
                <div class="hour_item">
                    <div id="time">6:45AM</div>
                    <div id="icon">
                        <img src="/src/assets/images/clear.png" /></div>
                    <div id="temperature">Sunrise</div>
                </div>
                <div class="hour_item">
                    <div id="time">7AM</div>
                    <div id="icon">
                        <img src="/src/assets/images/clear.png" /></div>
                    <div id="temperature">36°</div>
                </div>
                <div class="hour_item">
                    <div id="time">8AM</div>
                    <div id="icon">
                        <img src="/src/assets/images/clear.png" /></div>
                    <div id="temperature">38°</div>
                </div>

            </div>
            <div id="right_arrow">
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

        #hour_slides {
            display: flex;
            align-items: center;
            gap: $baseDistance * 4;
            overflow: hidden;
            width: 100%;

            .hour_item {
                display: flex;
                flex-direction: column;
                align-items: center;
                gap: $baseDistance;

                #icon {
                    img {
                        width: $baseDistance * 4;
                    }
                }
            }
        }
        
    }
</style>