<template>
    <Error
        v-if="error"
        :error="errorDisplay"
    />
    <ul class="list">
        <li
            v-for="item in statData"
            :key="item.label"
        >
            <Stat v-bind="item" />
        </li>
    </ul>

    <ul class="card-list">
        <li
            v-for="(item, index) in data.forecast.forecastday"
            :key="item.date"
        >
            <DayCard
                :temp="item.day.avgtemp_c"
                :date="new Date(item.date)"
                :weather-code="item.day.condition.code"
                :is-active="activeIndex == index"
                @click="() => emit('select-index', index)"
            >
                <IconSun />
            </DayCard>
        </li>
    </ul>

    <CitySelect />
</template>

<script setup>
import { computed } from "vue";
import CitySelect from "./CitySelect.vue";
import Error from "./Error.vue";
import DayCard from "./DayCard.vue";
import Stat from "./Stat.vue";
import { errorMap } from "../constants";

const { data, error, activeIndex } = defineProps({
    data: Object,
    error: Object,
    activeIndex: Number,
});

const emit = defineEmits(["select-index"]);

const statData = computed(() => {
    if (!data) {
        return [];
    }
    return [
        { label: "Влажность", stat: `${data.forecast.forecastday[activeIndex].day.avghumidity} %` },
        { label: "Облачность", stat: `${data.forecast.forecastday[activeIndex].day.daily_chance_of_rain} %` },
        {
            label: "Ветер",
            stat: `${Math.ceil((data.forecast.forecastday[activeIndex].day.maxwind_kph * 1000) / 3600)} м/c`,
        },
    ];
});

const errorDisplay = computed(() => {
    return errorMap.get(error?.error?.code);
});
</script>

<style lang="scss" scoped>
.list {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin-bottom: 70px;
}

.card-list {
    display: flex;
    justify-content: center;
    margin-bottom: 60px;
    gap: 2px;
}

.error {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 400px;
}
</style>
