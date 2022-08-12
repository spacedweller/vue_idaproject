<template>
    <div class="container">
        <div class="remove-icon" @click="remove()"></div>
        <div class="item-image">
            <img class="item-image" :src="link"/>
        </div>
        <div class="item-text-container">
            <div class="item-name"><p>{{id}} : {{name}}</p></div>
            <div class="item-description"><p>{{description}}</p></div>
            <div class="item-price"><p>{{Number.parseInt(price).toLocaleString('ru')}} руб.</p></div>
        </div>

    </div>
</template>
<script>
export default {
    name: 'CatalogueItem',
    props: ['id', 'name', 'description', 'link', 'price'],
    emits: ['id'],
    methods: {
    }
}
</script>
<style scoped>
    .container {
        position: relative;
        box-sizing: border-box;
        width: 332px;
        height: 423px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        margin: 0px 16px 16px 0px;
    }

    .remove-icon {
        position: absolute;
        top: -8px;
        right: -8px;
        width: 30px;
        height: 30px;
        background-color: red;
        z-index: 100;
        border-radius: 30%;
    }


    .item-image {
        box-sizing: border-box;
        width: 100%;
        height: 200px;
        border-radius: 4px 4px 0px 0px;
    }


    .item-text-container {
        padding: 16px;
    }
    .item-name {
        box-sizing: border-box;
        width: 100%;
        margin-bottom: 16px;

        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 600;
        font-size: 20px;
        line-height: 25px;

        color: #3F3F3F;
    }

    .item-description {
        box-sizing: border-box;
        width: 100%;
        height: 80px;
        
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 20px;
        margin-bottom: 32px;

        color: #3F3F3F;
    }

    .item-price {
        box-sizing: border-box;

        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 600;
        font-size: 24px;
        line-height: 30px;

        color: #3F3F3F;
    }


</style>