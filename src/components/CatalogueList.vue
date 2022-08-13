<template>
    <div v-cloak>
        <transition-group :duration="{ enter: 500, leave: 800 }" name="list" tag="div" class="shelf" v-if="catalogueList">
            <div class="list-item" v-for="(item, index) in catalogueList" v-bind:key="item">
                <CatalogueItem @removeItem="removeItem"
                               :id="index" :name="item.name"
                               :description="item.description"
                               :link="item.link"
                               :price="item.price"/>
            </div>
        </transition-group>
    </div>
</template>
<script>
import CatalogueItem from "./CatalogueItem.vue"

export default {
    name: 'CatalogueList',
    components: {CatalogueItem} ,
    props: ['catalogueList'],
    methods: {
        removeItem(id){
            this.$emit('removeItem', id)
        }
    }
}
</script>
<style>
.shelf {
    display: flex;
    width: 100%;
    padding-left: 16px;
    flex-flow: wrap;
    height: 100%;
}

.list-item {
    transition: all 1s;
    display: inline-block;
    margin-right: 10px;
}
.list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
}
.list-leave-active {
    position: absolute;
}


@media (max-width: 768px) {
    .shelf {
        align-items: center;
        margin: 0 auto;
        padding: 0;
        flex-flow: column;
    }

    .list-item {
        margin: 0 0 16px 0;

    }
}
</style>