<template>
    <div class="left__day-info day-info">
        <span class="day-info__day">{{ day }}</span>
        <span class="day-info__date">{{ date }}</span>
        <div class="day-info__location">
            <IconLocation :size="25" /><span>{{ city }}</span>
        </div>
    </div>
    <div class="left__day-info day-info">
        <div class="day-info__icon">
            <IconSun
                v-if="weatherCode <= 1003"
                :size="95"
            />
            <IconCloud
                v-if="weatherCode >= 1006 && weatherCode < 1063"
                :size="95"
            />
            <IconRain
                v-if="weatherCode >= 1063"
                :size="95"
            />
        </div>

        <span class="day-info__temp">{{ dayData.day.avgtemp_c }} °C</span>
        <span class="day-info__weather-info">{{ dayData.day.condition.text }}</span>
    </div>
</template>

<script setup>
import IconLocation from "../icons/IconLocation.vue";
import IconSun from "../icons/weather/IconSun.vue";
import IconCloud from "../icons/weather/IconCloud.vue";
import IconRain from "../icons/weather/IconRain.vue";
import { computed, inject } from "vue";
import { cityProvider } from "../constants";

const { dayData } = defineProps({
    dayData: Object,
});

const city = inject(cityProvider);
const weatherCode = computed(() => {
    return dayData.day.condition.code;
});
const day = computed(() => {
    return new Date(dayData.date).toLocaleDateString("ru-Ru", { weekday: "long" });
});

const date = computed(() => {
    return new Date(dayData.date).toLocaleDateString("ru-RU", {
        day: "numeric",
        month: "long",
        year: "numeric",
    });
});
</script>

<style lang="scss" scoped>
.day-info {
    display: flex;
    flex-direction: column;
    gap: 15px;

    &__location {
        display: flex;
        align-items: center;
        font-size: 20px;
        font-weight: 600;
        gap: 15px;
    }

    &__day {
        font-size: 37px;
        font-weight: 700;
        text-transform: capitalize;
    }

    &__date {
        font-size: 22px;
        font-weight: 500;
    }

    &__icon {
        margin-left: 25px;
        margin-bottom: 15px;
    }

    &__temp {
        font-size: 50px;
        font-weight: 700;
    }

    &__weather-info {
        font-size: 30px;
        font-weight: 700;
    }
}
</style>
