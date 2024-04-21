<script setup>
    import { ref, inject, watchEffect } from 'vue';

    // import function to register Swiper custom elements
    import { register } from 'swiper/element/bundle';
    // register Swiper custom elements
    register();

    const hoursObject = inject('hours')
    const hours = hoursObject.value
    let time = ref('')
    let hoursOnly = ref([])
    
    const timeProcessor = (time) => {
        time = parseInt(time.slice(11,13))

        if(time == 0) { return '12AM' }
        if(time == 12) { return '12PM' }

        // for AM time
        if(time > 0 && time < 12) {
            return time + 'AM'
        }

        // for PM time
        if(time > 12 && time <=23) {
            return (time - 12) + 'PM'
        }
    }

    watchEffect(() => {
        console.log(hours)
        // for(hour in hours.value) {
        //     console.log(hour)
        // }
    })
</script>

<template>
    <div id="hours">
        <button class="prev_arrow">
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
        </button>

        <swiper-container
            class="swiper_container"
            slides-per-view="5"
            grab-cursor="true"
            :navigation="{
                nextEl: '.next_arrow',
                prevEl: '.prev_arrow',
            }" >

            <!-- START LOOP -->
                <swiper-slide v-for="(hour, index) in hours" class="slide_item">
                    <div class="time">{{ timeProcessor(hour.time) }}</div>
                    <div class="icon">
                        <img src="/src/assets/images/clear.png" />
                    </div>
                    <div class="temperature">{{ Math.round(hour.temp_f) }}°</div>
                </swiper-slide>
            <!-- END LOOP -->
                
        </swiper-container>
        
        <button class="next_arrow">
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
        </button>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    #hours {
        display: flex;
        gap: $baseDistance * 2;
        margin-bottom: $baseDistance * 2;

        .swiper_container {
            // swiper-slide width would be overflow (huge width), the below code would fix it.
            width: 100%;
            max-width: 100%;
            max-height: 100vh;
            min-height: 0;
            min-width: 0;

            .slide_item {
                display: flex;
                flex-direction: column;
                text-align: center;
                gap: $baseDistance * 1.5;

                .icon {
                    img {
                        width: $baseDistance * 4;
                    }
                }
            }
        }

        .prev_arrow, .next_arrow{
            cursor: pointer;
            border: none;
            background-color: $cardContainerBackgroundColor;
        }
    }
</style>