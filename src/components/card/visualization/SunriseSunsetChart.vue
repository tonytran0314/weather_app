<script setup>
    import { onMounted } from 'vue'
    import Chart from 'chart.js/auto';

    onMounted(() => {
        const ctx = document.getElementById('sunrise_sunset_chart');
        const PI = Math.PI

        Chart.pluginService.register({
    beforeInit: function(chart) {
        // We get the chart data
        var data = chart.config.data;

        // For every dataset ...
        for (var i = 0; i < data.datasets.length; i++) {

            // For every label ...
            for (var j = 0; j < data.labels.length; j++) {

                // We get the dataset's function and calculate the value
                var fct = data.datasets[i].function,
                    x = data.labels[j],
                    y = fct(x);
                // Then we add the value to the dataset data
                data.datasets[i].data.push(y);
            }
        }
    }
});
        const labels = [
            0, 
            PI/8, 
            PI/4, 
            3*PI/8,

            PI/2, 

            5*PI/8, 
            3*PI/4, 
            7*PI/8, 

            PI,

            9*PI/8, 
            5*PI/4,
            11*PI/8, 

            3*PI/2,
            
            13*PI/8,
            7*PI/4, 
            15*PI/8,
            2*PI
        ];

        let data = {
            labels: labels, // x values
            datasets: [
                {
                    type: 'line',
                    function: function(x) {
                        return x
                    },
                    data: [],
                    borderWidth: 3,
                    fill: false
                },
                // {
                //     // below y = 0
                //     type: 'line',

                //     // y values
                //     // data: [
                //     //     -1, 
                //     //     -0.924, 
                //     //     -0.707, 
                //     //     -0.383,
                //     //     0, 
                //     //     NaN, NaN, NaN, NaN, NaN, NaN, NaN,
                //     //     0, 
                //     //     -0.383, 
                //     //     -0.707, 
                //     //     -0.924, 
                //     //     -1
                //     // ],
                //     // (0,-1)
                //     // (PI/4, -0.707)
                //     // ...
                //     borderWidth: 3,
                //     elements: {
                //         point: {
                //             radius: 0
                //         }
                //     },
                // },
                // {
                //     // above y = 0
                //     type: 'line',
                //     // data: [
                //     //     NaN, NaN, NaN, NaN, 
                //     //     0, 
                //     //     0.383,
                //     //     0.707,
                //     //     0.924, 
                //     //     1, 
                //     //     0.924,
                //     //     0.707,
                //     //     0.383, 
                //     //     0, 
                //     //     NaN, NaN, NaN, NaN
                //     // ],
                //     borderWidth: 3,
                //     elements: {
                //         point: {
                //             radius: 0
                //         }
                //     },
                // },
                // {
                //     // y = 0
                //     type: 'line',
                //     data: [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
                //     borderWidth: 5,
                //     elements: {
                //         point: {
                //             radius: 0
                //         }
                //     },
                // },
                // {
                //     type: 'scatter',
                //     data: [
                //         {
                //             x: 0,
                //             y: 0
                //         },
                //         {
                //             x: 2*PI,
                //             y: 0
                //         },
                //         {
                //             x: PI,
                //             y: 0
                //         },
                //         // CURRENT
                //         {
                //             x: 1,
                //             y: -0.54
                //         }
                //     ]
                // }
            ]
        }


        let options = {
            scales: {
                y: {
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
                    min: 0,
                    max: 20,
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
            tension: 0.5
        }
        

        new Chart(ctx, {
            data,
            options
        });
    })

    // const config = {
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