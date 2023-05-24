<template>
 
    <section class="main-home">
    
        <div class="container">
            <h2 class="category-title">{{$route.params.id}}</h2>
            <div class="card-handler">
              
          <MainHomeCards v-for="list in lists" :key="list" :item="list"></MainHomeCards>
            </div>
                </div>   

    </section>


</template>

<script>
import MainHomeCards from '@/components/MainHomeCards.vue';
export default {
    data() {
        return {
            lists: []
        };
    },
    methods:{
        fetching(id){
            fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${id}`)
            .then(data => data.json())
            .then(res => {
            this.lists = res.meals;
        })
            .catch(err => {
            console.log(err);
        });
        }
    },
    created() {
        this.fetching(this.$route.params.id)
        fetch('https://www.themealdb.com/api/json/v1/1/search.php?s=Arrabiata')
        .then(data=>data.json())
        .then(res=>{
            console.log(res);
        })
        .catch(err=>{
            console.log(err);
        })
    },
    watch:{
        $route(newVal){
            this.fetching(newVal.params.id)
        }
    },
    components: { MainHomeCards }
}
</script>

<style>

</style>