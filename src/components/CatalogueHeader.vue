<template>
    <div  class="catalogueheader">
        <div>
            <p>Добавление товара</p>
        </div>
        <div class="list-options">
            <button @click="clickSort()" class="dropdown-sort">{{filters.find(o => o.type === sorting).text}} &nbsp;&nbsp;&nbsp; </button>
            <ul class="sorting-list scale-in-top" v-if="opened" >
                <li  v-for="filter in filters"  class="sorting-option" @click="changeSorting(filter.type)" :key="filter.id">{{filter.text}}</li>
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
            opened: false,
            filters: [
                {type: 'default', text: 'По умолчанию'},
                {type: 'name', text: 'По названию'},
                {type: 'ascending', text: 'Дешевле'},
                {type: 'descending', text: 'Дороже'},
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
            console.log("HEADER sortingg tossed:", type)
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
        display: inherit;
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

    .dropdown-sort:after {
        box-sizing: border-box;
        content: '';
        position: absolute;
        border: 1px solid #B4B4B4;
        transform: rotate(45deg);
        width: 6.5px;
        height: 6.5px;
        transform: rotate(45deg);
        top: 12px;
        right: 15px;
        clip-path: inset(25% 0% 0 25%);
        -webkit-clip-path: inset(25% 0% 0 25%);
    }

    .sorting-list {
        width: 120px;
        position: absolute;
        background-color: white;
        list-style: none;
        padding: 0px;
        z-index: 1;
    }

    .sorting-option {
        width: 100%;
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
        height: 35px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .sorting-option:hover, .dropdown-sort:hover {
        background-color: #e96c6c;
        color: white;
    }

    .dropdown-sort:hover:after {
        border-color: white;
    }


.scale-in-top {
	-webkit-animation: scale-in-top 0.5s cubic-bezier(0.455, 0.030, 0.515, 0.955) both;
	animation: scale-in-top 0.5s cubic-bezier(0.455, 0.030, 0.515, 0.955) both;
}

@-webkit-keyframes scale-in-top {
  0% {
    -webkit-transform: scale(0);
            transform: scale(0);
    -webkit-transform-origin: 50% 0%;
            transform-origin: 50% 0%;
    opacity: 1;
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
    -webkit-transform-origin: 50% 0%;
            transform-origin: 50% 0%;
    opacity: 1;
  }
}
@keyframes scale-in-top {
  0% {
    -webkit-transform: scale(0);
            transform: scale(0);
    -webkit-transform-origin: 50% 0%;
            transform-origin: 50% 0%;
    opacity: 1;
  }
  100% {
    -webkit-transform: scale(1);
            transform: scale(1);
    -webkit-transform-origin: 50% 0%;
            transform-origin: 50% 0%;
    opacity: 1;
  }
}



</style>