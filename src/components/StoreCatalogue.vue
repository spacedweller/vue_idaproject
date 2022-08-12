<template>
    <CatalogueHeader @changeSorting="setSorted"/>
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
    name: 'StoreCatalogue',
    components: {
        CatalogueForms, CatalogueHeader, CatalogueList
    },
    data() {
        return {
            catalogueList: [],
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
        },
        setSorted(type){
            console.log("new sorting type", type)
            localStorage.setItem('sorting', type)
            if (type === 'default'){
                this.catalogueList.sort((v1, v2) => v1.index - v2.index).map((v) => v.name);
            }
            else if (type === 'name'){
                this.catalogueList.sort(function(a, b) { 
                    return a.name.localeCompare(b.name);
                });
            }
            else if (type === 'ascending'){
                this.catalogueList.sort((v1, v2) => v1.price - v2.price).map((v) => v.name);
            }
            else if (type === 'descending'){
                this.catalogueList.sort((v1, v2) => v2.price - v1.price).map((v) => v.name);
            }
        }
    },
    watch: {
        catalogueList: {
            handler(catalogueList){
                localStorage.setItem('catalogue_items', JSON.stringify(catalogueList))
            }
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