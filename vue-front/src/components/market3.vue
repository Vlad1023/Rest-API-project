<template>
    <section id="root">
        <ul v-for="item in goodsArr" :key="item.Name" id="market1">
            <li class="Name">{{ item.Name }}</li>
            <li class="Img">
            <div class= "Discount">
                <span v-if="item.Discount">-{{item.Discount}}%</span>
            </div><img v-bind:src="getImg(item.ImgData)"></li>
            <li><div @click="Purchase(item)" class="btn"><span>Добавить в корзину</span></div></li>
            <li class="Description">{{ item.Description }}</li>
        </ul>
    </section>
</template>
<script>
 import api from '@/API/api.js';
    export default {
        data: function () {
            return {
                goodsArr: Array,
            };
        },
        props: {
            itemArId: Number
        },
         created() {
            api.market((info) => {this.goodsArr = info;this.Swap(this.itemArId)},'market3');
             this.$eventBus.$on('market3Find', (Id) => {
            this.Swap(Id);
        });
         },
        methods: {
            getImg(toConvert) {
                return "data:image/jpg;base64," + toConvert;
            },
            Purchase(item){
                api.isLoggedForce( () => this.addItem(item));
            },
            addItem(item){
                if(!item["Discount"]) item["Discount"] = 0;
                api.addItemToCart(item);
            },
             Swap(Id){
                if(Id){
                let temp = this.goodsArr[0];
                this.goodsArr[0] = this.goodsArr[Id];
                this.goodsArr[Id] = temp;
                }
            }
        }
    };
</script>
<style scoped>
    html, body {
        box-sizing: border-box;
    }

    ul, li {
        padding: 0;
        margin: 0;
        list-style: none;
    }

    ul {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        width: 20%;
        padding: 10px;
        height: 90%;
    }

    #root {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: flex-start;
        padding: 2%;
        background-color: #3456A6;
        overflow-x: scroll;
    }
    .Name {
        font-size: 1.5rem;
    }
    .Description {
        font-size: 1rem;
    }
    .Name, .Description {
        color: #41D272;
        padding: 10px;
    }
    .Img {
        position: relative;
        width: 100%;
        align-content: center;
    }
    .Discount{
        border: 1px solid red;
        font-size: 1.5rem;
        position: absolute;
        top: 20px;
        left: 50%;
        color: red;
        transform: rotate(-45deg);
        font-family: cursive;
    }
    .Img img {
        display: block;
        margin-left: auto;
        margin-right: auto;
        max-height: 200px;
        width: auto;
        height: auto;
    }

    .btn {
        line-height: 50px;
        height: 50px;
        text-align: center;
        width: 250px;
        cursor: pointer;
    }

    .btn {
        color: #FFF;
        transition: all 0.3s;
        position: relative;
    }

    .btn span {
        transition: all 0.3s;
    }

        .btn::before {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            opacity: 0;
            transition: all 0.3s;
            border-top-width: 1px;
            border-bottom-width: 1px;
            border-top-style: solid;
            border-bottom-style: solid;
            border-top-color: rgba(255,255,255,0.5);
            border-bottom-color: rgba(255,255,255,0.5);
            transform: scale(0.1, 1);
        }

    .btn:hover span {
        letter-spacing: 2px;
    }

        .btn:hover::before {
            opacity: 1;
            transform: scale(1, 1);
        }

        .btn::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            transition: all 0.3s;
            background-color: rgba(255,255,255,0.1);
        }

    .btn:hover::after {
        opacity: 0;
        transform: scale(0.1, 1);
    }
</style>
