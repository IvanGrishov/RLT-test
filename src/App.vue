<template>
    <div class="inventory">
        <div class="inventory__wrapper">
            <inventory-sidebar></inventory-sidebar>
            <inventory-table></inventory-table>
        </div>
        <inventory-search></inventory-search>
    </div>
</template>

<script>

import InventorySidebar from "@/components/inventory-sidebar";
import InventorySearch from "@/components/inventory-search";
import InventoryTable from "@/components/inventory-table";
export default {
    name: 'App',
    components: {InventoryTable, InventorySearch, InventorySidebar}
}
</script>

<style lang="scss" src="./assets/null.scss"></style>
<style lang="scss">
    :root {
        --dark-color: #1E1E1E;
        --secondary-color: #262626;
        --white-color: #fff;

        --green-color: #7FAA65;
        --orange-color: #AA9765;
        --violet-color: #656CAA;
    }
    #app {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100%;
    }
    body {
        background: var(--dark-color);
        font-family: sans-serif;
    }
    h3 {
        color: white;
    }
    .inventory {
        max-width: 785px;
        width: 100%;
        height: 500px;
    }
    .inventory__wrapper {
        display: grid;
        grid-template-columns: 236px 525px;
        grid-gap: 0 24px;
        height: 100%;
    }


</style>
