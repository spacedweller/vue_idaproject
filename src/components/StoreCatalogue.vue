<template>
    <div>
        <CatalogueHeader @changeSorting="setSorted"/>
        <div class="catalogue-wrapper">
            <CatalogueForms @newForm="addItem"/>
            <CatalogueList @removeItem="removeItem" :catalogueList="catalogueList"/>
        </div>
    </div>
</template>

<script>
import CatalogueForms from "./CatalogueForms.vue"
import CatalogueHeader from "./CatalogueHeader.vue"
import CatalogueList from "./CatalogueList.vue"
import {initialArray} from "../extra.js"

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
        if (localStorage.getItem('catalogue_items') && localStorage.getItem('catalogue_items').length !== 2) {
            console.log("catalogue length", localStorage.getItem('catalogue_items').length)
            this.catalogueList = JSON.parse(localStorage.getItem('catalogue_items'))
        } else {
            console.log("initia array", initialArray)
            console.log("initia array", initialArray.length)
            this.catalogueList = initialArray
        }
    },
    methods: {
        removeItem(id){
            this.catalogueList.splice(id, 1);
            
        },
        addItem(form) {
            this.catalogueList = [...this.catalogueList, {name: form.name, description: form.description, link: form.link, price: form.price}]
        },
        setSorted(type){
            console.log("STORE sortingg tossed:", type)
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
                console.log("SORTING FUNCTION ASCENDING")
                this.catalogueList.sort((v1, v2) => v1.price - v2.price).map((v) => v.name);
            }
            else if (type === 'descending'){
                console.log("SORTING FUNCTION DESCENDING")
                this.catalogueList.sort((v1, v2) => v2.price - v1.price).map((v) => v.name);
            }

        }
    },
    watch: {
        catalogueList: {
            deep: true,
            handler(catalogueList){
                console.log("catalogue list SAVED")
                this.setSorted(localStorage.getItem('sorting'))
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

    @media (max-width: 768px) {
        .catalogue-wrapper {
            flex-direction: column;
            align-items: center;
    }
}
  
</style>