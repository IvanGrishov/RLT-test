<template>
    <div class="inventory__table inventory-table">
        <inventory-item
            v-for="item in items"
            @dragstart="startDrag($event, item)"
            @dragenter="enterDrag($event, item)"
            @dragend="endDrag($event, item)"
            @dragover="overDrag($event)"
            :draggable="item.empty === 0"
            :item="item"
            @showDesc="showDesc"
        >
        </inventory-item>
        <transition name="fade">
            <inventory-description
                v-if="isDescription"
                @closeDesc="closeDesc"
                :selectedItem="selectedItem"
                @deleteElems="deleteElems"
                @closeDescription="closeDesc"
            >
            </inventory-description>
        </transition>
    </div>
</template>

<script>
import InventoryItem from "@/components/inventory-item";
import InventoryDescription from "@/components/inventory-description";

let items = [
    { id: 0, count: 2, srcImg: 'green-square.png', empty: 0 },
    { id: 1, count: 14, srcImg: 'orange-square.png', empty: 0 },
    { id: 2, count: 8, srcImg: 'violet-square.png', empty: 0 },
    { id: 3, count: '', srcImg: '', empty: 1 },
    { id: 4, count: '', srcImg: '', empty: 1 },
    { id: 5, count: '', srcImg: '', empty: 1 },
    { id: 6, count: '', srcImg: '', empty: 1 },
    { id: 7, count: '', srcImg: '', empty: 1 },
    { id: 8, count: '', srcImg: '', empty: 1 },
    { id: 9, count: '', srcImg: '', empty: 1 },
    { id: 10, count: '', srcImg: '', empty: 1 },
    { id: 11, count: '', srcImg: '', empty: 1 },
    { id: 12, count: '', srcImg: '', empty: 1 },
    { id: 13, count: '', srcImg: '', empty: 1 },
    { id: 14, count: '', srcImg: '', empty: 1 },
    { id: 15, count: '', srcImg: '', empty: 1 },
    { id: 16, count: '', srcImg: '', empty: 1 },
    { id: 17, count: '', srcImg: '', empty: 1 },
    { id: 18, count: '', srcImg: '', empty: 1 },
    { id: 19, count: '', srcImg: '', empty: 1 },
    { id: 20, count: '', srcImg: '', empty: 1 },
    { id: 21, count: '', srcImg: '', empty: 1 },
    { id: 22, count: '', srcImg: '', empty: 1 },
    { id: 23, count: '', srcImg: '', empty: 1 },
    { id: 24, count: '', srcImg: '', empty: 1 },
]

export default {
    name: "inventory-table",
    components: {InventoryDescription, InventoryItem},
    data() {
        return {
            items: items,
            dragStartElem: null,
            dragEndElem: null,
            isDescription: false,
            selectedItem: {},
            countDeleteElems: null,
        }
    },
    methods: {
        startDrag(event, item) {
            this.dragStartElem = item

            this.changeStyle(event)
        },
        overDrag(event) {
            event.preventDefault();
        },
        enterDrag(event, item) {
            this.dragEndElem = item
        },
        endDrag(event) {
            event.target.classList.remove('table-cell__drag-start')

            let startElemIndex = this.items.findIndex(elem => elem.id === this.dragStartElem.id)
            let endElemIndex = this.items.findIndex(elem => elem.id === this.dragEndElem.id)

            items.splice(startElemIndex, 1, this.dragEndElem)
            items.splice(endElemIndex, 1, this.dragStartElem)

            this.items = [...items]

            this.saveLocalStorage()
        },
        changeStyle(event) {
            let borderRight = event.target.style.borderRight;
            let borderLeft = event.target.style.borderLeft;
            let borderBottom = event.target.style.borderBottom;
            let borderTop = event.target.style.borderTop;
            let borderRadius = event.target.style.borderRadius

            event.target.classList.add('table-cell__drag-start')

            event.target.style.border = '1px solid #4D4D4D'
            event.target.style.borderRadius ='24px'

            event.target.style.cursor = 'grab'

            setTimeout((function(borderRight, borderLeft, borderBottom, borderTop, borderRadius) {
                return function() {
                    event.target.style.borderRadius = borderRadius;

                    event.target.style.borderTop = borderTop
                    event.target.style.borderBottom = borderBottom
                    event.target.style.borderLeft = borderLeft
                    event.target.style.borderRight = borderRight
                }
            })(borderRight, borderLeft, borderBottom, borderTop, borderRadius), 1);
        },
        showDesc(item) {
            if (item.empty === 0) {
                this.isDescription = true
                this.selectedItem = item
            }
        },
        closeDesc() {

            this.isDescription = false
        },
        deleteElems(count) {
            this.selectedItem.count - count >= 0 ? this.selectedItem.count -= count : 0

            this.saveLocalStorage()
        },
        saveLocalStorage() {
            localStorage.setItem('InventoryItems', JSON.stringify(this.items));
        },
        getInventoryItems() {
            const itemsFromStorage = JSON.parse(localStorage.getItem('InventoryItems'));

            if (itemsFromStorage !== null) {
                items = itemsFromStorage
                this.items = [...itemsFromStorage]
            }
        }
    },
    mounted() {
        this.getInventoryItems()
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
        position: relative;
    }
    .table-cell {
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
        border-right: 1px solid #4D4D4D;
        border-bottom: 1px solid #4D4D4D;
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
        position: absolute;
        top: 0;
        left: 0;
        display: flex;
        justify-content: center;
        align-items: center;
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
        .table-cell__count {
            display: none;
        }
    }
    .table-cell__content {
        pointer-events: none;
    }
    .inventory-table__img-cursor-grab {
        position: absolute;
    }
    .inventory-description {
        border-radius: 0 24px 24px 0;
    }

    .fade-enter-active {
        transition: all 0.2s ease-out;
    }

    .fade-leave-active {
        transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1);
    }

    .fade-enter-from,
    .fade-leave-to {
        transform: translateX(100px);
    }
</style>
