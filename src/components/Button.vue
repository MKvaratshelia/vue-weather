<script setup></script>

<template>
    <button class="button"><slot /></button>
</template>
<style scoped lang="scss">
.button {
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background: var(--gradient);
    font-family: var(--font);
    font-size: 20px;
    font-weight: 600;
    color: var(--primary);
    padding: 14px;
    display: flex;
    gap: 9px;
    align-items: center;
    width: 100%;
    height: 52px;
    justify-content: center;

    &:hover {
        background: var(--gradient-inverted);
    }
}
</style>
