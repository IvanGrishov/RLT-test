<template>
    <div class="inventory__sidebar inventory-sidebar">
        <div class="inventory-sidebar__img-wrapper">
            <img class="inventory-sidebar__img" src="../assets/images/img-sidebar.jpg" alt="inventory-img">
        </div>
        <ul class="inventory-sidebar__list-elements">
            <li class="inventory-sidebar__elements inventory-sidebar__elements--big"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "inventory-sidebar"
}
</script>

<style lang="scss">
.inventory-sidebar {
    border: 1px solid #4D4D4D;
    border-radius: 12px;
    background-color: var(--secondary-color);
    padding: 18px 14px 24px;
    height: 100%;
}

.inventory-sidebar__img-wrapper {
    position: relative;
    height: 240px;
}

.inventory-sidebar__img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 8px;
}

.inventory-sidebar__list-elements {
    margin-top: 20px;
    padding-left: 9px;
    padding-right: 9px;
}

.inventory-sidebar__elements {
    background: linear-gradient(90deg, #3C3C3C 0%, #444444 51.04%, #333333 100%);
}

.inventory-sidebar__elements--big {
    width: 100%;
    height: 26px;
    border-radius: 8px;
    margin-bottom: 24px;
}

.inventory-sidebar__elements--small {
    border-radius: 4px;
    height: 10px;

    &:not(:last-child) {
        margin-bottom: 16px;
    }

    &:last-child {
        margin-top: 24px;
    }
}
</style>
