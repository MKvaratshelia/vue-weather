<template>
    <div class="stat">
        <p class="stat__name">{{ label }}</p>
        <p class="stat__value">{{ stat }}</p>
    </div>
</template>

<script setup>
const { label, stat } = defineProps({
    label: String,
    stat: String,
});
</script>

<style lang="scss" scoped>
.stat {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 16px;
    font-size: 28px;

    &__name {
        font-weight: 700;
        text-transform: uppercase;
    }

    &__value {
        font-weight: 500;
    }
}
</style>
