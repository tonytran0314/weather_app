<script setup>
    import { inject, watchEffect, ref } from 'vue';

    let pressureDegree = ref('')
    const pressure = inject('pressure')
    const LOWEST_DEGREE = -140
    const HIGHEST_DEGREE = 140
    const LOW_PRESSURE = 29.8
    const HIGH_PRESSURE = 30.2
    const TOTAL_DEGREE = Math.abs(LOWEST_DEGREE) + Math.abs(HIGHEST_DEGREE)
    const TOTAL_PRESSURE = Math.round((HIGH_PRESSURE - LOW_PRESSURE) * 10)/10 // round to 1 decimal

    const calculatepressureDegreeValue = (pressure) => {
        if(pressure < LOW_PRESSURE) {
            return LOWEST_DEGREE
        }

        if(pressure > HIGH_PRESSURE) {
            return HIGHEST_DEGREE
        }

        const differenceFromLowPressure = pressure - LOW_PRESSURE

        // 280 (total degree)   ~   0.4 (total pressure)
        // ? degree             ~   diffPressure pressure
        const correspondDegree = differenceFromLowPressure * TOTAL_DEGREE / TOTAL_PRESSURE

        // if the result is negative, the dot will be placed on the left side
        // if ... positive, ... right side
        return Math.round(LOWEST_DEGREE + correspondDegree) + 'deg'
    }

    watchEffect(() => {
        pressureDegree.value = calculatepressureDegreeValue(pressure.value)
    })
</script>

<template>
    <div id="pressure_chart_container" class="chart_item">
        <div id="pressure_circle">
            <div id="current_pressure">
                <span>{{ pressure }}</span>inHg
            </div>
            <div id="current_pressure_mark"></div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #pressure_chart_container {
        width: 100%;
        height: auto;
        display: flex;
        justify-content: center;
        padding: $baseDistance * 2 0 $baseDistance * 3 0;

        #pressure_circle {
            width: $baseDistance * 15;
            height: $baseDistance * 15;
            border-radius: 50%;
            border: 2px solid $white;
            border-bottom: 1px solid $mainBackgroundColor;
            position: relative;

            &::before {
                content: 'Low';
                position: absolute;
                bottom: -16px;
            }

            &::after {
                content: 'High';
                position: absolute;
                right: 0;
                bottom: -16px;
            }

            #current_pressure {
                width: $baseDistance * 12;
                height: $baseDistance * 12;
                background-color: $mainBackgroundColor;
                position: absolute;
                border-radius: 50%;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;

                span {
                    font-size: 1.8em;
                }
            }

            #current_pressure_mark {
                rotate: v-bind(pressureDegree); // PARAM

                width: 2px;
                height: 65px;
                position: absolute;
                left: 50%;
                top: 22%;
                transform: translate(-50%, -50%);

                &::before {
                    content: '';
                    width: 12px;
                    height: 12px;
                    background-color: $white;
                    position: absolute;
                    border-radius: 50%;
                    left: -5px;
                }
            }

        }
    }    
</style>