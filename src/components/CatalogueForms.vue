<template>
    <div class='sidebar'>
        <p class="input-description">Наименование товара<span class="star"></span></p>
        <form class="item-input" :class="{ 'invalid-input': valid.name != true && validation} ">
            <textarea v-model="forms.name" class="textarea-input shorten ghost-text" placeholder="Введите наименование товара"></textarea>
            <div class="validation-helper" v-if="valid.name != true && validation">Поле является обязательным</div>
        </form>

         <p class="input-description">Описание товара</p>
        <form class="item-input description" >
            <textarea v-model="forms.description" class="textarea-input ghost-text" placeholder="Введите описание товара"></textarea>
        </form>

         <p class="input-description">Ссылка на изображение товара<span class="star"></span></p>
        <form class="item-input" :class="{ 'invalid-input': valid.link != true && validation}">
            <textarea v-model="forms.link" class="textarea-input shorten ghost-text" placeholder="Введите ссылку"></textarea>
            <div class="validation-helper" v-if="valid.link != true && validation">Поле является обязательным</div>
        </form>

        <p class="input-description">Цена товара<span class="star"></span></p>
        <form class="item-input" :class="{ 'invalid-input': valid.price != true && validation}">
            <textarea v-model="forms.price" class="textarea-input shorten ghost-text" placeholder="Введите цену"></textarea>
            <div class="validation-helper" v-if="valid.price != true && validation">Поле является обязательным</div>
        </form>

        <button v-on:click="addItem()" :class="{'item-btn': activeButton, 'puff-out-center': activeButton, 'submit-button': activeButton == false}">Добавить товар</button>
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
            valid: {
                name: false,
                link: false,
                price: false,
            },
            validation: false,
            activeButton: false,
        }
    },
    name: 'CatalogueForms',
     created() {
        
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
                if (forms.name) {
                    localStorage.setItem('name', forms.name)
                    this.valid.name = true
                } else {
                    this.valid.name = false
                    localStorage.removeItem('name')
                }

                if (forms.description) {
                    localStorage.setItem('description', forms.description)
                } else {
                    localStorage.removeItem('description')
                }

                if (forms.link) {
                    localStorage.setItem('link', forms.link)
                    this.valid.link = true
                } else {
                    this.valid.link = false
                    localStorage.removeItem('link')
                }

                if (forms.price) {
                    localStorage.setItem('price', forms.price)
                    this.valid.price = true
                } else {
                    this.valid.price = false
                    localStorage.removeItem('price')
                }

                if (Object.values(this.valid).every(val => val === true)) { 
                    this.activeButton = true
                } else {
                    setTimeout(() => this.activeButton  = false, 300);
                    
                }

                if (Object.values(this.valid).every(val => val === false)) {
                    this.validation = false
                }
            }, deep: true}
    },
    methods: {
        addItem() {
            if (Object.values(this.valid).every(val => val === true)) {
                this.validation = false
                console.log("FORMS form is valid, adding new item to the catalogue")
                this.$emit('newForm', this.forms)
                localStorage.removeItem('name')
                localStorage.removeItem('desc')
                localStorage.removeItem('price')
                localStorage.removeItem('link')
                this.forms.name = ''
                this.forms.description = ''
                this.forms.link = ''
                this.forms.price = ''
            } else {
                this.validation = true
            }
        }
    }
    ,

}
</script>

<style scoped>
.sidebar {
    position: sticky;
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
    position: relative;
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
    position: relative;
}

.star::after {
    content: '';
    position: absolute;
    display: inline-block;
    width: 4px;
    height: 4px;
    background: #FF8484;
    border-radius: 50%
}

.item-input {
    position: relative;
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

.submit-button {
    width: 284px;
    height: 36px;
    border: none;
    background: #EEEEEE;
    border-radius: 10px;

    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;

    text-align: center;
    letter-spacing: -0.02em;

    color: #B4B4B4;

    margin-top: 8px;
}

.invalid-input {
    box-shadow: none;
    border: 1px solid #ff4949;
}

.validation-helper {
    position: absolute;
    left: -1px;
    top: 38px;
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 8px;
    line-height: 10px;
    /* identical to box height */

    letter-spacing: -0.02em;

    color: #FF8484;
}

.shorten {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.puff-out-center:focus {
	-webkit-animation: puff-out-center 1.5s cubic-bezier(0.165, 0.840, 0.440, 1.000) both;
	animation: puff-out-center 1.5s cubic-bezier(0.165, 0.840, 0.440, 1.000) both;
}

@-webkit-keyframes puff-out-center {
  0% {
    -webkit-transform: scale(1);
            transform: scale(1);
    -webkit-filter: blur(0px);
            filter: blur(0px);
    opacity: 1;
  }
  100% {
    -webkit-transform: scale(2);
            transform: scale(2);
    -webkit-filter: blur(4px);
            filter: blur(4px);
    opacity: 0;
  }
}
@keyframes puff-out-center {
  0% {
    -webkit-transform: scale(1);
            transform: scale(1);
    -webkit-filter: blur(0px);
            filter: blur(0px);
    opacity: 1;
  }
  100% {
    -webkit-transform: scale(2);
            transform: scale(2);
    -webkit-filter: blur(4px);
            filter: blur(4px);
    opacity: 0;
  }
}

@media (max-width: 768px) {
    .sidebar {
        position: initial;
        margin-bottom: 16px;
    }
}
</style>