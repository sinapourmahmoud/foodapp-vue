<template>
    <div class="card">
        <div class="card-img-handler">
            <img :src="`${item.strMealThumb}/preview`" alt="picture" class="card-img">
        </div>
        <div class="card-body">
            <router-link :to="`singlepage/${item.strMeal}`" class="card-food-title">{{item.strMeal}}</router-link>
        </div>
    </div>
</template>


<script>
export default {
        props:['item'],


}
</script>
<style>
.card-food-title{
    font-size: 14px;
    font-weight: 500;
    text-align: center;
    margin-top: 1rem;
    color: rgb(65, 64, 64);
}
.card-img{
    width: 100%;
    height: 100%;
    object-fit: cover;

}
.card{
    padding: 0.2rem;
    cursor: pointer;
    
}
.card-img-handler{
    width: 100%;
    height: 14rem;
    border-radius: 5px;
}
.card-img-handler img{
    border-radius: 5px;
}
</style>