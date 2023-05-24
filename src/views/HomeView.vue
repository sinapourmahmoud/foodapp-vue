<template>
 
<section class="main-home">
    
    <div class="container">
        <h2 class="category-title">Dessert</h2>
        <div class="card-handler">
          
        <MainHomeCards v-for="dessert in desserts" :item="dessert" :key="dessert"></MainHomeCards>
        </div>
            </div>   
            <div class="container">
        <h2 class="category-title">Beef</h2>
        <div class="card-handler">
          
        <MainHomeCards v-for="beef in beefs" :item="beef" :key="beef"></MainHomeCards>
        </div>
            </div> 
            <div class="container">
        <h2 class="category-title">Seafoods</h2>
        <div class="card-handler">
          
        <MainHomeCards v-for="Seafood in Seafoods" :item="Seafood" :key="Seafood"></MainHomeCards>
        </div>
            </div>
            <div class="button-handler">
            <router-link class="see-all" to="/category">See All Categories</router-link></div>
</section>


</template>

<script>
import MainHomeCards from '@/components/MainHomeCards.vue';


export default {
    components: { MainHomeCards }
    ,
data(){
    return{
  l:[{d:5}],
        desserts:[],
        Seafoods:[],
        beefs:[]
    }
},
methods:{
    categoryFetching(category,name){
            fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${category}`)
    .then(res=> res.json())
    .then(data=>{ console.log(data);
        name=data.meals.slice(0,4)
        console.log(name);

    })
    .catch(err=>{
        console.log(err);
    })
    }
},
created(){
// this.categoryFetching('beef',this.beefs)
// this.categoryFetching('Seafood',this.Seafoods)
fetch('https://www.themealdb.com/api/json/v1/1/filter.php?c=Dessert')
.then(data=> data.json())
.then(res=>{
    this.desserts=res.meals.slice(0,4)
   
})
.catch(err=> console.log(err))
fetch('https://www.themealdb.com/api/json/v1/1/filter.php?c=beef')
.then(data=> data.json())
.then(res=>{
    this.beefs=res.meals.slice(0,4)
   
})
.catch(err=> console.log(err))
fetch('https://www.themealdb.com/api/json/v1/1/filter.php?c=seafood')
.then(data=> data.json())
.then(res=>{
    this.Seafoods=res.meals.slice(0,4)
   
})
.catch(err=> console.log(err))

}

}
</script>
<style>
    .card-handler{
        margin: 1rem;
    }
    .card-handler{
        display: flex;
        align-items: flex-start;
        gap: 1rem;
        justify-content: space-between;
flex-wrap: wrap;
    }
    .see-all{

        padding: 4px 8px;
        border-radius: 5px;
        background-color: #464646;
        color: white;
        font-size: 17px;
    }
    .button-handler{
        display: flex;
        align-items: center;
        justify-content: center;
        margin:1rem 0 2rem ;
    }
@media screen and (min-width:768px){
.card{
    flex: 0 1 23%;
}
}
@media screen and (max-width:768px){
    .card{
        flex: 0 1 100%;
     
    }
}
</style>
