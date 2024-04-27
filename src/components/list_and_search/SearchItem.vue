<script setup>
    const props = defineProps({
        'name': {
            type: String
        },
        'region': {
            type: String
        },
        'country': {
            type: String
        }
    })
</script>

<template>
    <div class="search_item">
        <span v-show="name">{{ name }}</span>
        <span v-show="region">, {{ region }}</span>
        <span v-show="country">, {{ country }}</span>
    </div>
</template>

<style lang="scss" scoped>

    @import '/src/assets/variables';

    .search_item {
        padding: $baseDistance * 2 $baseDistance * 3;
        transition: .2s;

        &:hover {
            background-color: $labelColor;
            border-radius: $baseDistance;
            cursor: pointer;
        }
    }
    
</style>