<script setup>
  import { inject } from 'vue';

  const days = inject('days')
  
  const date = new Date()
  const currentDay = date.getDay()
  const DAYS = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
</script>

<template>
  <div class="detail_item" id="days">
    <div class="title_container">
      <div class="title_icon">
        <svg
          width="16px"
          height="16px"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M3 9H21M7 3V5M17 3V5M6 12H8M11 12H13M16 12H18M6 15H8M11 15H13M16 15H18M6 18H8M11 18H13M16 18H18M6.2 21H17.8C18.9201 21 19.4802 21 19.908 20.782C20.2843 20.5903 20.5903 20.2843 20.782 19.908C21 19.4802 21 18.9201 21 17.8V8.2C21 7.07989 21 6.51984 20.782 6.09202C20.5903 5.71569 20.2843 5.40973 19.908 5.21799C19.4802 5 18.9201 5 17.8 5H6.2C5.0799 5 4.51984 5 4.09202 5.21799C3.71569 5.40973 3.40973 5.71569 3.21799 6.09202C3 6.51984 3 7.07989 3 8.2V17.8C3 18.9201 3 19.4802 3.21799 19.908C3.40973 20.2843 3.71569 20.5903 4.09202 20.782C4.51984 21 5.07989 21 6.2 21Z"
            stroke="rgb(98, 116, 139)"
            stroke-width="2"
            stroke-linecap="round"
          />
        </svg>
      </div>
      <div class="title">DAILY FORECAST</div>
    </div>
    <div id="days_forecast">
      <!-- Start loop -->
      <div v-for="(day, index) in days" class="days_forecast_item">
        <div class="date">{{ DAYS[currentDay+index] }}</div>
        <div class="day_weather_status_icon">
          <img :src="day.day.condition.icon" />
          <!-- <img src="/src/assets/images/clear.png" /> -->
        </div>
        <div class="temperature_range">
          <div class="day_highest_temperature">{{ Math.round(day.day.maxtemp_f) }}°</div>
          <div class="day_lowest_temperature">{{ Math.round(day.day.mintemp_f) }}°</div>
        </div>
      </div>
      <!-- End loop -->

    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "/src/assets/variables";

#days {
  display: flex;
  flex-direction: column;
  gap: $baseDistance;

  #days_forecast {
    display: flex;
    flex-direction: column;
    gap: $baseDistance;

    .days_forecast_item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-top: 1px solid $labelColor;
      padding-top: $baseDistance;

      .day_weather_status_icon {
        img {
          width: $baseDistance * 4;
        }
      }

      .temperature_range {
        display: flex;
        gap: $baseDistance * 2;

        .temperature_bar {
          display: flex;
          align-items: center;
        }
      }
    }
  }
}
</style>
