<template>
  <div class="cat-card">
    <div class="cat-img">
        <img :src="`${item.strCategoryThumb}`" alt="">
    </div>
    <router-link class="cat-title" :to="`/category/${item.strCategory}`">{{item.strCategory}}</router-link>
  </div>
</template>

<script>
export default {
props:['item']
}
</script>

<style>
.cat-title{
    font-size: 17px;
    color: rgb(65, 64, 64);

}
.cat-img{
    width: 240px;
    height: 240px;
    position: relative;
    border-radius: 50%;
    overflow: hidden;
    
}
.cat-img::before{
    position: absolute;
    content: "";
    top: 0;
    left: 0;
    height: 100%;
    z-index: 10;
    border-radius: 50%;
    opacity: 0;
    transition: opacity 0.5s ease-in;
    width: 100%;
    background-color: rgba(0,0,0,.3);
}
.cat-card:hover .cat-img::before{
    opacity: 1;
}
.cat-card:hover .cat-img img{
    transform: scale(1.1);
}
.cat-img img{
    width: 100%;
    border-radius: 50%;
    height: 100%;
    transition: transform 0.5s ease-in;

    object-fit: cover;
    
}
.cat-card{
    cursor: pointer;
}
</style>