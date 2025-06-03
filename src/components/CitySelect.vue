<template>
    <div class="city-select">
        <div
            v-if="isEdited"
            class="city-select__input"
        >
            <Input
                placeholder="Введите город"
                type="text"
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
import { ref } from "vue";
import Input from "./Input.vue";
const isEdited = ref(false);
const emit = defineEmits({
    selectCity(payload) {
        return payload;
    },
});

function select() {
    isEdited.value = false;
    emit("selectCity", "london");
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
