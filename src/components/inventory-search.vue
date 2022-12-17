<template>
    <div class="inventory__search inventory-search">
        <div class="inventory__search-field"></div>
        <svg class="inventory-search__icon-close" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M18 7.05L16.95 6L12 10.95L7.05 6L6 7.05L10.95 12L6 16.95L7.05 18L12 13.05L16.95 18L18 16.95L13.05 12L18 7.05Z" fill="white"/>
        </svg>
    </div>
</template>

<script>
export default {
    name: "inventory-search"
}
</script>

<style>
    .inventory-search {
        height: 72px;
        padding: 18px 68px 18px 18px;
        background: var(--secondary-color);
        border: 1px solid #4D4D4D;
        border-radius: 12px;
        margin-top: 24px;
        position: relative;
    }
    .inventory__search-field {
        background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
        box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
        border-radius: 12px;
        height: 100%;
    }
    .inventory-search__icon-close {
        position: absolute;
        top: 8px;
        right: 8px;
        cursor: pointer;
    }
</style>
