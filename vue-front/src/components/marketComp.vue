<template>
<div>
<div class="menu">
    <router-link class = "vue-nav" to="/market1">Каталог товаров</router-link>
    <router-link class = "vue-nav" to="/market2">Акции</router-link>
    <router-link class = "vue-nav" to="/market3">Популярное</router-link>
</div>
<div id= "menuContent"><router-view></router-view></div>
</div>
</template>
<script>
export default {

}
</script>
<style scoped>
.menu{
width: 100%;
border:1px solid black;
list-style: none;
margin: 0;
padding: 0;
display: flex;
justify-content: space-between;
}
.vue-nav  {
box-sizing: border-box;
font-size: 1.5rem;
color:white;
font-weight: 100;
letter-spacing: 2px;
text-decoration: none;
background:rgba(0,0,0,0.2);
padding:20px 5px;
display: inline-block;
width: 100%;
text-align: center;
transition:all 0.5s;
color: green;
}
.vue-nav:hover {
background: rgba(0,0,0,0.3);
}
#menuContent{
box-sizing: border-box;
padding: 5% 10% 0;
}
</style>