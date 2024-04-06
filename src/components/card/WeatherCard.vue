<script setup>
    import Overview from './Overview.vue';
    import Details from './Details.vue';
</script>

<template>
    <div id="weather_card">
        <Overview />
        <Details />
    </div>
</template>

<style lang="scss" scoped>

    @import '../../assets/variables';

    #weather_card {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>