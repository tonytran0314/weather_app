<script setup>
    import { onMounted } from 'vue'
    import Chart from 'chart.js/auto';

    onMounted(() => {
        const ctx = document.getElementById('sunrise_sunset_chart');
        const PI = Math.PI
        const DATA_COUNT = 6.5;
        const labels = [];

        for (let i = 0; i < DATA_COUNT; i=i+0.5) {
            labels.push(i.toString());
        }
        labels.push(6.28)

        let data = {
            labels: labels, // x values
            datasets: [
                {
                    data: [-1, -0.878, -0.54, -0.071, 0.416, 0.801, 0.99, 0.936, 0.654, 0.211, -0.284, -0.709, -0.96, -0.977], // y values
                    // (0,-1)
                    // (0.5, -0.878)
                    // ...
                    borderWidth: 1
                },
                {
                    data: [0,0,0,0,0,0,0,0,0,0,0,0,0,0], // y values
                    borderWidth: 1
                }
            ]
        }


        let options = {
            scales: {
                y: {
                    // backgroundColor: "#FFFFFF",
                    min: -1,
                    max: 1.3,
                    ticks: {
                        display: false
                    },
                    grid: {
                        display: false
                    },
                    border: {
                        display: false
                    }
                },
                x: {
                    // backgroundColor: "#FFFFFF",
                    min: 0,
                    max: 4*PI,
                    ticks: {
                        display: false
                    },
                    grid: {
                        display: false
                    },
                    border: {
                        display: false
                    }
                }
            },
            plugins: {
                legend: {
                    display: false
                },
                tooltips: {
                    enable: false
                }
            },
            elements: {
                point: {
                    radius: 0
                }
            },
            tension: 0.5
        }
        

        new Chart(ctx, {
            type: 'line',
            data,
            options
        });
    })

    // const config = {
    //     type: 'line',
    //     data: {},
    //     options: {},
    //     plugins: []
    // }
</script>

<template>
    <canvas id="sunrise_sunset_chart"></canvas>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #sunrise_sunset_chart {
        // background-color: gray;
    }
    
</style>