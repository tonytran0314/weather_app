<script setup>
    import { inject, computed } from 'vue';
    const windMph = inject('windMph')
    const windDegree = inject('windDegree')
</script>

<template>
    <div id="wind_chart_container" class="chart_item">
        <div id="compass_circle">
            <div id="north" class="direction">N</div>
            <div id="east" class="direction">E</div>
            <div id="south" class="direction">S</div>
            <div id="west" class="direction">W</div>

            <div id="compass_center">
                <span>{{ windMph }}</span>
                mph
            </div>
            <div id="wind_direction_arrow"></div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #wind_chart_container {
        width: 100%;
        height: auto;
        // padding: $baseDistance * 2;

        #compass_circle {
            width: $baseDistance * 15;
            height: $baseDistance * 15;
            // background-color: yellow;
            border: 2px solid $white;
            border-radius: 50%;
            position: relative;

            .direction {
                width: $baseDistance * 3;
                height: $baseDistance * 3;
                background-color: $mainBackgroundColor;
                border-radius: 50%;
                display: flex;
                justify-content: center;
                align-items: center;
                position: absolute;
            }

            #north {
                left: 50%;
                transform: translate(-50%, -12px);
            }

            #east {
                right: 0;
                top: 50%;
                transform: translate(12px, -50%);
            }

            #south {
                bottom: 0;
                left: 50%;
                transform: translate(-50%, 12px);
            }

            #west {
                top: 50%;
                transform: translate(-12px, -50%);
            }

            #compass_center {
                width: $baseDistance * 6;
                height: $baseDistance * 6;
                background-color: $mainBackgroundColor;
                border-radius: 50%;
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                z-index: 2;
                display: flex;
                justify-content: center;
                align-items: center;
                text-align: center;
                font-size: 0.9em;
                flex-direction: column;
            }
            

            #wind_direction_arrow {
                rotate: 20deg; // PARAM 

                width: 2px;
                height: 80px;
                background-color: $white;
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                z-index: 1;
                transform-origin: 0 0;

                // arrow tail (circle)
                &::before {
                    content: '';
                    background-color: $white;
                    width: $baseDistance;
                    height: $baseDistance;
                    position: absolute;
                    border-radius: 50%;
                    bottom: 0;
                    left: 50%;
                    transform: translate(-45%, 8px);

                }

                // arrow head (triangle)
                &::after {
                    content: '';
                    position: absolute;
                    top: 0;
                    left: 50%;
                    transform: translate(-45%, -8px);
                    
                    width: 0;  
                    height: 0;  
                    border-left: 4px solid transparent; 
                    border-right: 4px solid transparent; 
                    border-bottom: 8px solid $white; 
                }
            }
        }
    }
</style>