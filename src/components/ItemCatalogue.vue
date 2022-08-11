<template>
    <CatalogueHeader/>
    <div class="catalogue-wrapper">
        <CatalogueForms @newForm="addItem"/>
        <CatalogueList :catalogueList="catalogueList"/>
    </div>
</template>

<script>
import CatalogueForms from "./CatalogueForms.vue"
import CatalogueHeader from "./CatalogueHeader.vue"
import CatalogueList from "./CatalogueList.vue"

export default {
    name: 'ItemCatalogue',
    components: {
        CatalogueForms, CatalogueHeader, CatalogueList
    },
    data() {
        return {
            catalogueList: []
        }
    },
    created(){
        if (localStorage.getItem('catalogue_items')) {
            this.catalogueList = JSON.parse(localStorage.getItem('catalogue_items'))
        }
    },
    methods: {
        addItem(form) {
            this.catalogueList = [...this.catalogueList, {name: form.name, description: form.description, link: form.link, price: form.price}]
        }
    }
}
</script>

<style scoped>
.catalogue-wrapper {
    display: flex;
    width: 100%;
}
  
</style>