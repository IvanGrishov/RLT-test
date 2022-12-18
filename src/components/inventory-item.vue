<template>
    <div
        class="table-cell"
         @click="showDesc(item)"
        :class="{'inventory-table__filled' : item.empty === 0}"
    >
        <div class="table-cell__content" :class="item.nameClass">
            <div class="table-cell__img" v-if="item.srcImg">
                <img :src=" require('../assets/images/' + item.srcImg) " alt="">
            </div>
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
    },
    methods: {
        showDesc(item) {
            this.$emit('showDesc', item)
        }
    }
}
</script>

<style lang="scss">
    .table-cell__img {
        width: 54px;
        height: 54px;
    }
    .inventory-table__filled {
        cursor: pointer;
        &:active {
            cursor: grab;
        }
    }
</style>
