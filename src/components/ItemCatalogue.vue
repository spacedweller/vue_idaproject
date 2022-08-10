<template>
    <CatalogueHeader/>
    <div class="catalogue-wrapper">
        <CatalogueForms/>
        <CatalogueList/>
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
    }
}
</script>

<style scoped>
.catalogue-wrapper {
    display: flex;
    width: 100%;
}
  
</style>