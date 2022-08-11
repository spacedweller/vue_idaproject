<template>
    <div class='sidebar'>
        <p class="input-description">Наименование товара<span class="star">*</span></p>
        <form class="item-input">
            <textarea v-model="forms.name" class="textarea-input ghost-text" placeholder="Введите наименование товара"></textarea>
        </form>
         <p class="input-description">Описание товара</p>
        <form class="item-input description">
            <textarea v-model="forms.description" class="textarea-input ghost-text" placeholder="Введите описание товара"></textarea>
        </form>
         <p class="input-description">Ссылка на изображение товара<span class="star">*</span></p>
        <form class="item-input">
            <textarea v-model="forms.link" class="textarea-input ghost-text" placeholder="Введите ссылку"></textarea>
        </form>
        <p class="input-description">Цена товара<span class="star">*</span></p>
        <form class="item-input">
            <textarea v-model="forms.price" class="textarea-input ghost-text" placeholder="Введите цену"></textarea>
        </form>
        <button v-on:click="addItem()" class="item-btn">Добавить товар</button>
    </div>
</template>

<script>
export default {
    data() {
    return {
      forms: {
        name: '',
        description: '',
        link: '',
        price: '',
      },
      catalogue_items: [],
    }
  },
    name: 'CatalogueForms',
     created() {
        if (localStorage.getItem('catalogue_items')){
            console.log("catalogue exists")
            this.catalogue_items = JSON.parse(localStorage.getItem('catalogue_items'))
        }
        if (localStorage.getItem('name')){
            console.log("localstorage name exists")
            this.forms.name = localStorage.getItem('name')
            this.forms.description = localStorage.getItem('desc')
            this.forms.price = localStorage.getItem('price')
            this.forms.link = localStorage.getItem('link')
        } else {
            console.log("localstorage name is null")
            localStorage.setItem('name', '')
            localStorage.setItem('desc', '')
            localStorage.setItem('link', '')
            localStorage.setItem('price', '')
        }
      
    },
    watch: {
        forms: {
            handler(forms) {
                localStorage.setItem('name', forms.name)
                localStorage.setItem('desc', forms.description)
                localStorage.setItem('price', forms.price)
                localStorage.setItem('link', forms.link)
            }, deep: true}
    },
    methods: {
        addItem() {
            this.catalogue_items = [...this.catalogue_items, {name: this.forms.name, description: this.forms.description, link: this.forms.link, price: this.forms.price}]
            localStorage.setItem('catalogue_items', JSON.stringify(this.catalogue_items))
            this.$emit('newForm', this.forms)
            localStorage.removeItem('name')
            localStorage.removeItem('desc')
            localStorage.removeItem('price')
            localStorage.removeItem('link')
            this.forms.name = ''
            this.forms.description = ''
            this.forms.link = ''
            this.forms.price = ''
    }
    }
    ,

}

console.log(localStorage)
localStorage.removeItem('ghj')

</script>

<style scoped>
.sidebar {
    box-sizing: border-box;
    width: 332px;
    height: 440px;
    left: 32px;
    top: 83px;
    padding: 24px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    }

.input-description {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485E;
    margin-bottom: 4px;
}

.star {
    color: red;
}

.item-input {
    box-sizing: border-box;
    height: 36px;
    width: 100%;
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border: none;
    margin-bottom: 16px;
    padding: 8px 16px 8px 14px;
}

.ghost-text {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
}

.description {
    height: 108px;
}

.textarea-input {
    height: 100%;
    width: 100%;
    border: none;
    overflow: auto;
    outline: none;

    -webkit-box-shadow: none;
    -moz-box-shadow: none;
    box-shadow: none;

    resize: none; 
}
.item-btn {
    width: 284px;
    height: 36px;
    border:none;
    background: #7BAE73;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;

    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;

    text-align: center;
    letter-spacing: -0.02em;

    color: #FFFFFF;

    margin-top: 8px;
}

</style>