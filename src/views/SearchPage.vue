<template>
 
    <section class="main-home">
    
        <div class="container">
            <h2 class="category-title">{{$route.params.id}}</h2>
            <div v-if="lists">
            <div class="card-handler">
              
          <MainHomeCards v-for="list in lists" :key="list" :item="list"></MainHomeCards>
            </div></div>
            <div v-else>
                <h2 class="category-title">No results</h2>
            
            </div>
                </div>   

    </section>
</template>

<script>
import MainHomeCards from'./../components/MainHomeCards.vue'
export default {
    components:{
        MainHomeCards
    },
    data(){
        return{
            lists:[]
        }
    },
    methods:{
        fetching(id){
            fetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${id}`)
    .then(data=>data.json())
    .then(res=>{
       this.lists=res.meals
       console.log(this.lists);
    })
    .catch(err=>{
        console.log(err);
    })
        }
    },
created(){
this.fetching(this.$route.params.id)
},
watch:{
    $route(newval){
        this.fetching(newval.params.id)
    }
}
}
</script>

<style>

</style>