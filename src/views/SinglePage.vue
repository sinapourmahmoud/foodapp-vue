<template>
 
  <section class="inside-main">
    <div class="container">
      <div class="box-container">
        <div class="box-item picture-part">
<img :src="`${lists[0].strMealThumb}/preview`" alt="">
        </div>
        <div class="box-item content-part">
          <p class="title-box">{{lists[0].strMeal}}</p>
          <div class="gap-box">
            <div class="infos">
              <ul class="strIngredient-list" v-if="products">
                <li class="strIngredient-item">What you need ?</li>
                <li class="strIngredient-item" v-for="strIngredient in strIngredients" :key="strIngredient">{{strIngredient[1]}}</li>
              </ul>
              <ul class="strIngredient-list" v-if="!products">
                <li class="strIngredient-item">Measures</li>
                <li class="strIngredient-item" v-for="strMeasure in strMeasures" :key="strMeasure">{{strMeasure[1]}}</li>
              </ul>
          
          <small class="country text-muted">country: {{lists[0].strArea}}</small>
          <small class="country text-muted" style="margin-left:0.5rem">country: {{lists[0].strCategory}}</small>
        </div>
        <div class="option-buttons">
          <a href="#" class="option-btn" @click.prevent="products=true">Products</a>
          <a href="#" class="option-btn" @click.prevent="products=false">How to cook</a>
        </div>
        </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
data(){
  return{
    lists:[],
    strIngredients:[],
    strMeasures:[],
    products:true,
  }
},
created(){
  fetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${this.$route.params.id}`)
  .then(res=> res.json())
  .then(data=>{
    this.lists=data.meals
   Object.entries(this.lists[0]).forEach(item=> {
    if(item[0].indexOf('strIngredient')!=-1 && item[1]!='' && item[1]!=null){
      this.strIngredients.push(item)
    }
    else if(item[0].indexOf('strMeasure')!=-1 && item[1]!='' && item[1]!=null){
      this.strMeasures.push(item)
    }
   })
   console.log(this.lists[0]);
   console.log(this.strMeasures);

  })
  .catch(err=>{
    console.log(err);
  })
}
}
</script>

<style>

.picture-part{
  width: 40%;
  
  height: 10rem;
 
}
.picture-part img{
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.content-part{
 
  width: 100%;
}
.title-box{
  font-size: 19px;
}
.strIngredient-item{
  font-size: 14px;
  color: #555;
  margin-top: 0.5rem;
}
.gap-box{
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
}
.option-btn{
  margin-inline: 0.5rem;
  font-size: 15px;
  border: 1px solid #555;
  padding: 4px 8px;
  border-radius: 5px;
}
.option-btn:first-child{
  color: #555;
}
.option-btn:last-child{
  background-color: #555;
  color: white;
}
@media screen and (min-width:768px){
  .box-container{
  display: flex;
  align-items: flex-start;
  justify-content: center;
  width: 60rem;
  margin-inline: auto;
  gap: 3rem;
  
}
}
@media screen and (max-width:768px){
  .box-container{
    display: flex;
    flex-direction: column;
  }
  .picture-part{
    width: 100%;
  }
.gap-box{
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.option-buttons{
  order: 1;
  margin-top:1rem ;
}
.infos{
  order: 2;
}
}
</style>