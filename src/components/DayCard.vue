<template>
    <button
        class="day-card"
        :class="{ active: isActive }"
    >
        <IconSun
            v-if="weatherCode <= 1003"
            :color="iconColor"
        />
        <IconCloud
            v-if="weatherCode >= 1006 && weatherCode < 1063"
            :color="iconColor"
        />
        <IconRain
            v-if="weatherCode >= 1063"
            :color="iconColor"
        />
        <p class="day-card__day">{{ date.toLocaleDateString("ru-Ru", { weekday: "short" }) }}</p>
        <p class="day-card__temp">{{ temp }} °C</p>
    </button>
</template>

<script setup>
import { computed } from "vue";
import IconSun from "../icons/weather/IconSun.vue";
import IconCloud from "../icons/weather/IconCloud.vue";
import IconRain from "../icons/weather/IconRain.vue";

const { weatherCode, temp, date, isActive } = defineProps({
    weatherCode: Number,
    temp: Number,
    date: Date,
    isActive: Boolean,
});

const iconColor = computed(() => {
    return isActive ? "var(--color-primary-inverted)" : "var(--color-primary)";
});
</script>

<style lang="scss" scoped>
.day-card {
    display: flex;
    // height: 172px;
    gap: 15px;
    padding: 20px 24px;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    background-color: var(--color-bg-card);
    box-shadow: 1px 2px 4px 0px var(--color-bg-main);
    border-radius: 10px;
    cursor: pointer;
    color: var(--color-primary);

    &:not(.active):hover {
        background-color: var(--color-card-hover);
    }

    &__day {
        font-size: 20px;
        font-weight: 400;
    }

    &__temp {
        font-size: 20px;
        font-weight: 700;
    }
}
.active {
    background-color: var(--color-primary);
    color: var(--color-primary-inverted);
}
</style>
