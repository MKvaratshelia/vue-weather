<script setup>
import CitySelect from "./components/CitySelect.vue";
import Stat from "./components/Stat.vue";
import { computed, ref } from "vue";

function getCity(city) {
    city;
}
const data = ref({
    humidity: 90,
    rain: 0,
    wind: 3,
});

const dataModified = computed(() => {
    return [
        { label: "ВЛАЖНОСТЬ", stat: `${data.value.humidity}%` },
        { label: "ОСАДКИ", stat: `${data.value.rain}%` },
        { label: "ВЕТЕР", stat: `${data.value.wind} м/ч` },
    ];
});
</script>

<template>
    <main class="main">
        <ul class="list">
            <li
                v-for="item in dataModified"
                :key="item.label"
            >
                <Stat v-bind="item" />
            </li>
        </ul>

        <CitySelect @select-city="getCity" />
    </main>
</template>

<style scoped>
.main {
    display: flex;
    flex-direction: column;
    background-color: var(--color-bg-main);
    padding: 60px 50px;
    border-radius: 25px;
}

.list {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin-bottom: 70px;
}
</style>
