<template>
    <div class="inventory-description">
        <svg @click="closeDesc" class="inventory-description__icon-close" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"><path d="M18 7.05L16.95 6L12 10.95L7.05 6L6 7.05L10.95 12L6 16.95L7.05 18L12 13.05L16.95 18L18 16.95L13.05 12L18 7.05Z" fill="white"></path></svg>
        <div class="inventory-description__img">
            <img :src=" require('../assets/images/' + selectedItem.srcImg) " alt="">
        </div>
        <ul class="inventory-description__text">
            <li class="inventory-sidebar__elements inventory-sidebar__elements--big"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
            <li class="inventory-sidebar__elements inventory-sidebar__elements--small"></li>
        </ul>
        <div class="inventory-description__bottom-wrapper">
            <i-button
                v-if="isForm"
                class="inventory-description__delete-btn"
                @click="isForm = false"
            >
                Удалить предмет
            </i-button>
            <div v-else
                 class="inventory-description__form desc-form">
                <input
                    class="desc-form__input"
                    type="text"
                    placeholder="Введите количество"
                    v-model="countDeleteElems"
                    @input="$event.target.value = $event.target.value.replace(/[^0-9]/g, '')"
                >
                <div class="desc-form__btns">
                    <i-button class="desc-form__btn-cancel"
                              @click="cancelDelete"
                    >
                        Отмена
                    </i-button>
                    <i-button
                        class="desc-form__btn-confirm"
                        @click="deleteElems"
                    >
                        Подтвердить
                    </i-button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import IButton from "@/components/UI/i-button";

export default {
    name: "inventory-description",
    props: {
        selectedItem: {
            type: Object
        }
    },
    data() {
        return {
            isForm: true,
            countDeleteElems: null,
        }
    },
    components: {
        IButton
    },
    methods: {
        cancelDelete() {
            this.isForm = true;

            this.$emit('closeDescription')
        },
        closeDesc() {
            this.$emit('closeDesc')
        },
        deleteElems() {
            this.$emit('deleteElems', this.countDeleteElems);
        }
    }
}
</script>

<style lang="scss">
.inventory-description {
    display: flex;
    flex-direction: column;
    background: rgba(38, 38, 38, 0.5);
    border-left: 1px solid #4D4D4D;
    backdrop-filter: blur(8px);
    width: 250px;
    height: 100%;
    position: absolute;
    top: 0;
    right: 0;
    padding: 0 15px 18px 15px;
}

.inventory-description__img {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 215px;
    img {
        width: 130px;
        height: 130px;
    }
}

.inventory-description__text {
    padding: 16px 4px 24px;
    border-top: 1px solid #4D4D4D;
}

.inventory-description__delete-btn {
    margin-top: auto;
    background-color: var(--warning-color);
    color: var(--white-color);
    padding: 11px;
    &:hover {
        background-color: darken(#FA7272, 8%);
    }
}

.desc-form__input {
    font-family: 'Inter', sans-serif;
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 17px;
    padding: 11px 55px 12px 12px;
    background: var(--secondary-color);
    border: 1px solid var(--muted-color);
    border-radius: 4px;
    color: var(--white-color);
    width: 100%;
}

.desc-form__btns {
    margin-top: 20px;
    display: grid;
    grid-template-columns: 44% calc(56% - 10px);
    grid-gap: 0 10px;
    width: 100%;
}
.desc-form__btn-cancel {
    color: #2D2D2D;
    background-color: var(--white-color);
    padding: 8px;
    &:hover {
        background-color: darken(#fff, 70%);
        color: #fff;
    }
}
.desc-form__btn-confirm {
    color: var(--white-color);
    background-color: var(--warning-color);
    padding: 8px;
    &:hover {
        background-color: darken(#FA7272, 10%);
    }
}

.inventory-description__bottom-wrapper {
    padding-top: 20px;
    position: absolute;
    bottom: 18px;
    width: calc(100% - 30px);
    background: rgba(38, 38, 38, 0.6);
    z-index: 1;
    &::before {
        content: '';
        position: absolute;
        top: 0;
        left: -15px;
        width: calc(100% + 30px);
        height: 100%;
        border-top: 1px solid var(--muted-color);
        pointer-events: none;
    }
}
.inventory-description__icon-close {
    position: absolute;
    top: 8px;
    right: 8px;
    cursor: pointer;
    transition: var(--transition);
    path {
        transition: var(--transition);
    }
    &:hover {
        stroke: var(--warning-color)
    }
}
</style>
