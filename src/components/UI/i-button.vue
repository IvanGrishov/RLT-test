<template>
    <button class="i-btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: "my-button"
}
</script>

<style lang="scss">
    .i-btn {
        font-family: 'SF Pro Display', sans-serif;
        font-style: normal;
        font-weight: 400;
        font-size: 14px;
        line-height: 17px;
        width: 100%;
        border-radius: 8px;
        transition: var(--transition);
    }
</style>
