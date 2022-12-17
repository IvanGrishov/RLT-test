<template>
    <div class="table-cell">
        <div class="table-cell__content" :class="item.nameClass">
            <div class="table-cell__img"></div>
            <div class="table-cell__count" v-if="!item.empty">
                <span class="table-cell__count-number">{{ item.count }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "inventory-item",
    props: {
        item: {
            type: Object
        }
    }
}
</script>

<style scoped>

</style>
