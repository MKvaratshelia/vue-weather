<script setup>
import { onMounted, provide, ref, watch } from "vue";
import LeftPanel from "./components/Leftpanel.vue";
import RightPanel from "./components/RightPanel.vue";
import { cityProvider, API_ENDPOINT } from "./constants";

const data = ref(null);
const error = ref(null);
const activeIndex = ref(0);
const city = ref("Москва");

provide(cityProvider, city);

watch(city, () => {
    getCity(city.value);
});

onMounted(() => {
    getCity(city.value);
});

async function getCity(city) {
    const params = new URLSearchParams({
        q: city,
        lang: "ru",
        key: "5bb70e65fc754c21822185440250306",
        days: 3,
    });

    const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);

    if (res.status !== 200) {
        error.value = await res.json();
        data.value = null;
        return;
    }
    error.value = null;
    data.value = await res.json();
}
</script>

<template>
    <main class="main">
        <div class="left">
            <LeftPanel
                v-if="data"
                :day-data="data?.forecast.forecastday[activeIndex]"
            />
        </div>
        <div class="right">
            <RightPanel
                v-if="data"
                :active-index="activeIndex"
                :data
                :error
                @select-index="(i) => (activeIndex = i)"
            />
        </div>
    </main>
</template>

<style lang="scss" scoped>
.main {
    display: flex;
    align-items: center;
}

.left {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 66px;
    padding: 48px 32px 64px;
    width: 490px;
    height: 666px;
    border-radius: 30px;
    color: var(--color-primary);
    background: var(--gradient);
}
.right {
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: var(--color-bg-main);
    padding: 60px 50px;
    border-radius: 0 25px 25px 0;
}
</style>
