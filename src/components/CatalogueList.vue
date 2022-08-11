<template>
    <div class="shelf" v-if="catalogueList">
        <div v-for="(item, index) in catalogueList" v-bind:key="index">
            <CatalogueItem :id="index" :name="item.name" :description="item.description" :link="item.link" :price="item.price"/>
        </div>
    </div>
</template>
<script>
import CatalogueItem from "./CatalogueItem.vue"

export default {
    name: 'CatalogueList',
    components: { CatalogueItem },
        props: ['catalogueList']
        }

</script>
<style>
    .shelf {
        display: flex;
        width: 100%;
        padding-left: 16px;
        flex-flow: wrap;
    }
</style>