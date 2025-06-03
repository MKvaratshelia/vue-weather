<template>
    <input class="input" />
</template>

<script setup></script>

<style lang="scss" scoped>
.input {
    width: 260px;
    background: var(--color-bg-card);
    padding: 15px 20px;
    font-size: 18px;
    font-weight: 400;
    box-shadow: 1px 2px 4px 0px var(--color-bg-main);
    border: none;
    border-radius: 10px;
    outline: none;
    color: var(--color-primary);

    &::placeholder {
        color: var(--color-text-placeholder);
    }
}
</style>
