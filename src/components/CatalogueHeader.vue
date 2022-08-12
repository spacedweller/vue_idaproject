<template>
    <div  class="catalogueheader">
        <div>
            <p>Добавление товара</p>
        </div>
        <div class="list-options">
            <button @click="clickSort()" class="dropdown-sort">{{filters.find(o => o.type === sorting).text}}</button>
            <ul class="sorting-list" v-if="opened" >
                <li  v-for="filter in filters"  class="dropdown-sort sorting-option" @click="changeSorting(filter.type)" :key="filter.id">{{filter.text}}</li>
            </ul>
        </div>

    </div>
</template>
<script>
export default {
    name: 'CatalogueHeader',

    data(){
        return {
            sorting: 'default',
            translation: 'По умолчанию',
            opened: false,
            filters: [
                {type: 'default', text: 'По умолчанию'},
                {type: 'name', text: 'По названию'},
                {type: 'ascending', text: 'По возрастанию цены'},
                {type: 'descending', text: 'По убыванию цены'},
            ]
        }
    },
    created(){
        if (localStorage.getItem('sorting')){
            this.sorting = localStorage.getItem('sorting')
            this.changeSorting(this.sorting)
        }
    },
    methods: {
        changeSorting(type){
            this.sorting = type
            this.$emit('changeSorting', type)
            this.opened = false;
        },
        clickSort(){
            this.opened = !this.opened
        }
    }
}
</script>
<style scoped>
    .catalogueheader {
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 600;
        font-size: 28px;
        line-height: 35px;
        margin-bottom: 16px;
        display: flex;
        justify-content: space-between;
        color: #3F3F3F;
    }

    .list-options {
        width: 120px;
        height: 35px;
        position: relative;
    }

    .dropdown-sort {
        width: 100%;
        height: 100%;
        border: none;
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgb(0 0 0 / 10%);
        border-radius: 4px;
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
        text-decoration: none;
        user-select: none;
    }

    .sorting-list {
        width: 120px;
        position: absolute;
        background-color: white;
        list-style: none;
        padding: 0px;
    }

    .sorting-option {
        height: 35px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

</style>