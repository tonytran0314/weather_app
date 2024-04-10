<script setup>
    
</script>

<template>

    <div class="bar_container">
        <div class="temp_range">
            <div class="gradient">
                <div class="current_temp"></div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    .bar_container {
        width: 100px;
        height: 8px;
        background-color: $labelColor;
        border-radius: $baseDistance;
        position: relative;

        .temp_range {
            width: 56%;
            height: 100%;
            border-radius: $baseDistance;
            overflow: hidden;
            margin-left: 32%;
            position: absolute;


            .gradient {
                width: 100px;
                height: 100%;
                background-image: linear-gradient(to right, cyan, cyan, orange);
                border-radius: $baseDistance;
                position: absolute;
                left: -56%;

                .current_temp {
                    width: 8px;
                    height: 100%;
                    background-color: white;
                    border-radius: 50%;
                    border: 1px solid black;
                    margin-left: 55%;
                }
            }
        }
    }
    
</style>