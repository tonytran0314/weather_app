<script setup>
    import { inject, ref, watch, watchEffect } from "vue";
    import Bar from "../visualization/Bar.vue";

    const ALERTED_UV = 4;
    const sunProtectionPeriod = ref([])

    const isDay = inject('isDay')
    const hours = inject('hours')
    const uv = inject('uv')
    const uvLabel = ref('')
    const uvDescription = ref('')


    watchEffect(() => {
        if(uv.value >= 0 && uv.value < 3) {
            uvLabel.value = "Low"
        } 
        if(uv.value >= 3 && uv.value < 6) {
            uvLabel.value = "Moderate"
        } 
        if(uv.value >= 6 && uv.value < 8) {
            uvLabel.value = "High"
        } 
        if(uv.value >= 8 && uv.value < 11) {
            uvLabel.value = "Very High"
        } 
        if(uv.value >= 11) {
            uvLabel.value = "Extreme"
        } 


        for (let i in hours.value) {
            if(hours.value[i].uv >= ALERTED_UV) {
                sunProtectionPeriod.value.push(i)
            }
        }
        
        const timeConverter = (time) => {
            if(time > 12) {
                time = time - 12
                return time + ":00PM"
            }
            return time + ":00AM"
        }

        const sunProtectionFrom = timeConverter(sunProtectionPeriod.value[0])
        const sunProtectionTo = timeConverter(sunProtectionPeriod.value[sunProtectionPeriod.value.length - 1])

        let uvDayDescription = "Use sun protection from "+ sunProtectionFrom +" to " + sunProtectionTo
        const uvNightDescription = "Low for the rest of the day"
        
        
        uvDescription.value = isDay == '1' ? uvDayDescription : uvNightDescription
    })
</script>

<template>
    <div class="detail_item row_item" id="uv_index">
        <div class="title_container">
            <div class="title_icon">
                <svg width="16px" height="16px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M17 12C17 14.7614 14.7614 17 12 17C9.23858 17 7 14.7614 7 12C7 9.23858 9.23858 7 12 7C14.7614 7 17 9.23858 17 12Z" fill="rgb(98, 116, 139)"/>
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M12 1.25C12.4142 1.25 12.75 1.58579 12.75 2V4C12.75 4.41421 12.4142 4.75 12 4.75C11.5858 4.75 11.25 4.41421 11.25 4V2C11.25 1.58579 11.5858 1.25 12 1.25ZM3.66865 3.71609C3.94815 3.41039 4.42255 3.38915 4.72825 3.66865L6.95026 5.70024C7.25596 5.97974 7.2772 6.45413 6.9977 6.75983C6.7182 7.06553 6.2438 7.08677 5.9381 6.80727L3.71609 4.77569C3.41039 4.49619 3.38915 4.02179 3.66865 3.71609ZM20.3314 3.71609C20.6109 4.02179 20.5896 4.49619 20.2839 4.77569L18.0619 6.80727C17.7562 7.08677 17.2818 7.06553 17.0023 6.75983C16.7228 6.45413 16.744 5.97974 17.0497 5.70024L19.2718 3.66865C19.5775 3.38915 20.0518 3.41039 20.3314 3.71609ZM1.25 12C1.25 11.5858 1.58579 11.25 2 11.25H4C4.41421 11.25 4.75 11.5858 4.75 12C4.75 12.4142 4.41421 12.75 4 12.75H2C1.58579 12.75 1.25 12.4142 1.25 12ZM19.25 12C19.25 11.5858 19.5858 11.25 20 11.25H22C22.4142 11.25 22.75 11.5858 22.75 12C22.75 12.4142 22.4142 12.75 22 12.75H20C19.5858 12.75 19.25 12.4142 19.25 12ZM17.0255 17.0252C17.3184 16.7323 17.7933 16.7323 18.0862 17.0252L20.3082 19.2475C20.6011 19.5404 20.601 20.0153 20.3081 20.3082C20.0152 20.6011 19.5403 20.601 19.2475 20.3081L17.0255 18.0858C16.7326 17.7929 16.7326 17.3181 17.0255 17.0252ZM6.97467 17.0253C7.26756 17.3182 7.26756 17.7931 6.97467 18.086L4.75244 20.3082C4.45955 20.6011 3.98468 20.6011 3.69178 20.3082C3.39889 20.0153 3.39889 19.5404 3.69178 19.2476L5.91401 17.0253C6.2069 16.7324 6.68177 16.7324 6.97467 17.0253ZM12 19.25C12.4142 19.25 12.75 19.5858 12.75 20V22C12.75 22.4142 12.4142 22.75 12 22.75C11.5858 22.75 11.25 22.4142 11.25 22V20C11.25 19.5858 11.5858 19.25 12 19.25Z" fill="rgb(98, 116, 139)"/>
</svg>
            </div>
            <div class="title">UV INDEX</div>
        </div>
        <div class="row_item_body">
            <div id="uv_index_overview">
                <div id="uv_index_value">{{ uv }}</div>
                <div id="uv_index_status">{{ uvLabel }}</div>
            </div>
            <Bar :value="uv" />
            <div>{{ uvDescription }}</div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

    @import "/src/assets/variables";

    #uv_index_value {
        font-size: 2.5em;
    }

    #uv_index_status {
        font-size: 1.2em;
    }
    
</style>