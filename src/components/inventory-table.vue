<template>
    <div class="inventory__table inventory-table">
        <inventory-item
            v-for="item in items"
            @dragstart="startDrag($event, item)"
            @dragenter="enterDrag($event, item)"
            @dragend="endDrag($event, item)"
            :draggable="item.empty === 0"
            :item="item"
        >
        </inventory-item>
    </div>
</template>

<script>
import InventoryItem from "@/components/inventory-item";
const items = [
    { id: 0, count: 2, nameClass: 'table-cell__content--green', empty: 0 },
    { id: 1, count: 14, nameClass: 'table-cell__content--orange', empty: 0 },
    { id: 2, count: 8, nameClass: 'table-cell__content--violet', empty: 0 },
    { id: 3, count: '', nameClass: '', empty: 1 },
    { id: 4, count: '', nameClass: '', empty: 1 },
    { id: 5, count: '', nameClass: '', empty: 1 },
    { id: 6, count: '', nameClass: '', empty: 1 },
    { id: 7, count: '', nameClass: '', empty: 1 },
    { id: 8, count: '', nameClass: '', empty: 1 },
    { id: 9, count: '', nameClass: '', empty: 1 },
    { id: 10, count: '', nameClass: '', empty: 1 },
    { id: 11, count: '', nameClass: '', empty: 1 },
    { id: 12, count: '', nameClass: '', empty: 1 },
    { id: 13, count: '', nameClass: '', empty: 1 },
    { id: 14, count: '', nameClass: '', empty: 1 },
    { id: 15, count: '', nameClass: '', empty: 1 },
    { id: 16, count: '', nameClass: '', empty: 1 },
    { id: 17, count: '', nameClass: '', empty: 1 },
    { id: 18, count: '', nameClass: '', empty: 1 },
    { id: 19, count: '', nameClass: '', empty: 1 },
    { id: 20, count: '', nameClass: '', empty: 1 },
    { id: 21, count: '', nameClass: '', empty: 1 },
    { id: 22, count: '', nameClass: '', empty: 1 },
    { id: 23, count: '', nameClass: '', empty: 1 },
    { id: 24, count: '', nameClass: '', empty: 1 },
]

export default {
    name: "inventory-table",
    components: {InventoryItem},
    data() {
        return {
            items: items,
            itemID: null,
            dragStartElem: {},
            dragEndElem: {},
            changeItems: []
        }
    },
    methods: {
        startDrag(event, item) {
            this.dragStartElem = item

            event.target.classList.add('table-cell__drag-start')
        },
        enterDrag(event, item) {
            this.dragEndElem = item
        },
        endDrag(event, item) {
            let startElems = this.items.find(elem => elem.id === this.dragStartElem.id)
            let endElems = this.items.find(elem => elem.id === this.dragEndElem.id)

           items.forEach(item => {
                if (item.id === this.dragStartElem.id) {
                    item.id = endElems.id
                    item.count = endElems.count
                    item.nameClass = endElems.nameClass
                    item.empty = endElems.empty
                }
               if (item.id === this.dragEndElem.id) {
                   console.log(item)
                   item.id = startElems.id
                   item.count = startElems.count
                   item.nameClass = startElems.nameClass
                   item.empty = startElems.empty
               }
            })

            console.log(items)

            // console.log(this.items)
            // console.log(this.dragStartElem)
            // console.log(this.dragEndElem)
        }
    }
}
</script>

<style lang="scss">
    .inventory-table {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        width: 100%;
        border-radius: 12px;
        border: 1px solid #4D4D4D;
        overflow: hidden;
    }
    .table-cell {
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
        border-right: 1px solid #4D4D4D;
        border-bottom: 1px solid #4D4D4D;
        cursor: pointer;
        &:nth-child(5n) {
            border-right: none;
        }
        &:nth-last-child(-n+5) {
            border-bottom: none;
        }
    }
    .table-cell__content {
        width: 100%;
        height: 100%;
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .table-cell__content--green,
    .table-cell__content--orange,
    .table-cell__content--violet {
        .table-cell__img {
            width: 48px;
            height: 48px;
            position: absolute;
            &::before {
                content: '';
                position: absolute;
                top: 6px;
                width: 48px;
                height: 48px;
            }
            &::after {
                content: '';
                position: absolute;
                top: 0;
                right: -6px;
                width: 48px;
                height: 48px;
            }
        }
    }
    .table-cell__content--green {
        .table-cell__img {
            &::before {
                background: var(--green-color);
            }
            &::after {
                background: rgba(184, 217, 152, 0.35);
                backdrop-filter: blur(6px);
            }
        }
    }
    .table-cell__content--orange {
        .table-cell__img {
            &::before {
                background: var(--orange-color);
            }
            &::after {
                background: rgba(217, 187, 152, 0.35);
                backdrop-filter: blur(6px);
            }
        }
    }
    .table-cell__content--violet {
        .table-cell__img {
            &::before {
                background: var(--violet-color);
            }
            &::after {
                background: rgba(116, 129, 237, 0.35);
                backdrop-filter: blur(6px);
            }
        }
    }
    .table-cell__count {
        position: absolute;
        right: 0;
        bottom: 0;
        padding: 2px 4px;
        border-radius: 6px 0 0 0;
        border: 1px solid #4D4D4D;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .table-cell__count-number {
        font-weight: 500;
        font-size: 10px;
        color: var(--white-color);
        opacity: 0.4;
    }
    .table-cell__drag-start {
        border: 1px solid #4D4D4D;
        border-radius: 24px;
        padding: 23px;
        width: 105px;
        height: 100px;
        .table-cell__count {
            display: none;
        }
    }
</style>
