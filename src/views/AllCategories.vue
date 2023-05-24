<template>
<section class="main-category">

<div class="container">
  <h2 class="category-title">Category List</h2>

  <div class="flex-category">
 <CategoryCards v-for="category in allCategory" :item="category" :key="category"></CategoryCards>
  </div>
</div>
</section>
</template>
<script>
import CategoryCards from '@/components/CategoryCards.vue';

export default {
  components:{ CategoryCards },
  data(){
    return{
      allCategory:[]
    }
  },
  created(){
    fetch('https://www.themealdb.com/api/json/v1/1/categories.php')
    .then(data=> data.json())
    .then(res=> {
      console.log(res);
      this.allCategory=res.categories
    })
    .catch(err=>{
      console.log(err)
    })
  }

}
</script>
<style>
.cat-card{
  display: flex;
  flex-direction: column;
  gap: 1rem ;
  align-items: center;
}
@media screen and (min-width:768px) {
  .flex-category{
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    flex-wrap: wrap;
    gap: 1.5rem;
  }
  .cat-card{
    flex: 0 1 23%;
    margin: 1rem 0;
  }
}
@media screen and (max-width:768px) {
  
  .flex-category{
    display: flex;
    justify-content: space-between;
  
   flex-direction: column;
    gap: 1.5rem;
  }
  .cat-card{
margin: 1rem auto;
   
  }
}


</style>
