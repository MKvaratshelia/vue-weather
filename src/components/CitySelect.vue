<template>
    <div class="city-select">
        <div
            v-if="isEdited"
            class="city-select__input"
        >
            <Input
                v-model="inputvalue"
                v-focus
                placeholder="Введите город"
                type="text"
                @keyup.enter="select"
            />
            <Button @click="select">Сохранить</Button>
        </div>
        <Button
            v-else
            @click="edit"
            ><IconLocation />Изменить город</Button
        >
    </div>
</template>

<script setup>
import IconLocation from "../icons/IconLocation.vue";
import Button from "./Button.vue";
import { inject, ref } from "vue";
import Input from "./Input.vue";
import { cityProvider } from "../constants";
const isEdited = ref(false);

const city = inject(cityProvider);
const inputvalue = ref(city.value);

function select() {
    isEdited.value = false;
    city.value = inputvalue.value;
}

function edit() {
    isEdited.value = true;
}
</script>

<style lang="scss" scoped>
.city-select {
    width: 415px;
    &__input {
        display: flex;
        align-items: center;
        gap: 12px;
    }
}
</style>
