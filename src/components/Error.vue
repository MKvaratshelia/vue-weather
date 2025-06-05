<template>
    <p
        v-if="props.error"
        class="error"
    >
        {{ props.error }}
    </p>
</template>

<script setup>
const props = defineProps({
    error: String,
});
</script>

<style lang="scss" scoped>
.error {
    padding: 15px 52px;
    border-radius: 0px 0px 25px 25px;
    background: var(--color-bg-card);
    box-shadow: 1px 2px 4px 0px #222831;
    color: var(--color-primary);
    font-weight: 400;
    font-size: 18px;
}
</style>
