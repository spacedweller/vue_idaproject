<template>
    <transition appear name="slide-fade">
        <div v-cloak class="container"  @mouseover="hovered = true" @mouseleave="hovered = false">
            <div v-if="hovered" class="remove-icon" @click="remove(id)"></div>
            <div class="item-image">
                <img class="item-image" :src="link"/>
            </div>
            <div class="item-text-container">
                <div class="item-name"><p>{{name}}</p></div>
                <div class="item-description"><p>{{description}}</p></div>
                <div class="item-price"><p>{{Number.parseInt(price).toLocaleString('ru')}} руб.</p></div>
            </div>

        </div>
    </transition>
</template>
<script>
export default {
    name: 'CatalogueItem',
    props: ['id', 'name', 'description', 'link', 'price'],
    data(){
        return {
            hovered: false
        }
    },
    methods: {
        remove(id){
            this.$emit('removeItem', id)
        }
    },

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
    cursor: pointer;
}

.remove-icon {
    position: absolute;
    top: -8px;
    right: -8px;
    width: 30px;
    height: 30px;
    background-color: #FF8484;
    z-index: 100;
    border-radius: 30%;
    display: flex;
}

.remove-icon:after {
    content: url("data:image/svg+xml,%3Csvg width='14' height='16' viewBox='0 0 14 16' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.56294 4.76335V13.9953C1.56294 14.541 1.76303 15.0534 2.11256 15.4211C2.46048 15.7898 2.94467 15.9991 3.4514 16H10.541C11.0478 15.9991 11.532 15.7898 11.8798 15.4211C12.2293 15.0534 12.4294 14.541 12.4294 13.9953V4.76335C13.1242 4.57893 13.5745 3.90768 13.4815 3.19471C13.3884 2.48189 12.7811 1.94867 12.0622 1.94852H10.1437V1.48014C10.1459 1.08626 9.99017 0.708039 9.71134 0.42979C9.4325 0.151688 9.0537 -0.0031709 8.65982 4.92333e-05H5.33255C4.93867 -0.0031709 4.55986 0.151688 4.28103 0.42979C4.00219 0.708039 3.84646 1.08626 3.84865 1.48014V1.94852H1.93019C1.21122 1.94867 0.603931 2.48189 0.51084 3.19471C0.417896 3.90768 0.868128 4.57893 1.56294 4.76335ZM10.541 15.2506H3.4514C2.81075 15.2506 2.31236 14.7002 2.31236 13.9953V4.79629H11.68V13.9953C11.68 14.7002 11.1816 15.2506 10.541 15.2506ZM4.59806 1.48014C4.59558 1.28503 4.67227 1.09724 4.81074 0.959502C4.94906 0.821768 5.13729 0.746095 5.33255 0.749461H8.65982C8.85508 0.746095 9.04331 0.821768 9.18163 0.959502C9.32009 1.09709 9.39679 1.28503 9.3943 1.48014V1.94852H4.59806V1.48014ZM1.93019 2.69793H12.0622C12.4347 2.69793 12.7367 2.99989 12.7367 3.3724C12.7367 3.74491 12.4347 4.04688 12.0622 4.04688H1.93019C1.55768 4.04688 1.25571 3.74491 1.25571 3.3724C1.25571 2.99989 1.55768 2.69793 1.93019 2.69793Z' fill='white'/%3E%3C/svg%3E%0A");
    width: 30px;
    height: 30px;
    justify-content: center;
    position: absolute;
    top: 7px;
    left: 7px;
    
}


.item-image {
    box-sizing: border-box;
    width: 100%;
    height: 200px;
    border-radius: 4px 4px 0px 0px;
    object-position: bottom;
    object-fit: cover;
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
    overflow: hidden;
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

.remove-icon:hover {
-webkit-animation: shake-bottom 0.4s cubic-bezier(0.455, 0.030, 0.515, 0.955) both;
animation: shake-bottom 0.4s cubic-bezier(0.455, 0.030, 0.515, 0.955) both;
}

@-webkit-keyframes shake-bottom {
  0%,
  100% {
    -webkit-transform: rotate(0deg);
            transform: rotate(0deg);
    -webkit-transform-origin: 50% 100%;
            transform-origin: 50% 100%;
  }
  10% {
    -webkit-transform: rotate(2deg);
            transform: rotate(2deg);
  }
  20%,
  40%,
  60% {
    -webkit-transform: rotate(-4deg);
            transform: rotate(-4deg);
  }
  30%,
  50%,
  70% {
    -webkit-transform: rotate(4deg);
            transform: rotate(4deg);
  }
  80% {
    -webkit-transform: rotate(-2deg);
            transform: rotate(-2deg);
  }
  90% {
    -webkit-transform: rotate(2deg);
            transform: rotate(2deg);
  }
}
@keyframes shake-bottom {
  0%,
  100% {
    -webkit-transform: rotate(0deg);
            transform: rotate(0deg);
    -webkit-transform-origin: 50% 100%;
            transform-origin: 50% 100%;
  }
  10% {
    -webkit-transform: rotate(2deg);
            transform: rotate(2deg);
  }
  20%,
  40%,
  60% {
    -webkit-transform: rotate(-4deg);
            transform: rotate(-4deg);
  }
  30%,
  50%,
  70% {
    -webkit-transform: rotate(4deg);
            transform: rotate(4deg);
  }
  80% {
    -webkit-transform: rotate(-2deg);
            transform: rotate(-2deg);
  }
  90% {
    -webkit-transform: rotate(2deg);
            transform: rotate(2deg);
  }
}


.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

   [v-cloak] {
    display: block;
    padding: 50px 0;
}

@keyframes spinner {
    to {
        transform: rotate(360deg);
    }
}

[v-cloak]:before {
    content: "";
    box-sizing: border-box;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 20px;
    height: 20px;
    margin-top: -10px;
    margin-left: -10px;
    border-radius: 50%;
    border: 2px solid #ccc;
    border-top-color: #333;
    animation: spinner 0.6s linear infinite;
    text-indent: 100%;
    white-space: nowrap;
    overflow: hidden;
}

[v-cloak]>* {
    display: none;
}

@media (max-width: 768px) {
    .container {
        margin: 0px 0px 16px 0px;
    }
}

</style>