<template>
  <header>
    <div class="container">
        <h3 class="logo">Sina Food APP</h3>
        <div class="search-div">
            <form>
                <input type="text" class="search-input" placeholder="add Your favorite food!" v-model="input">
                <router-link :to="`/search/${input}`" class="submit" @click.prevent="clearInput()"><i class='bx bx-search-alt-2'></i></router-link>
            </form>
        </div>
        <div class="options-div">
            <router-link :to="`/category/${list.strCategory}`" class="option-bar" v-for="list in lists" :key="list">
                <i class='bx bx-bowl-hot'></i>
                {{list.strCategory
                }}
            </router-link>

        </div>
    </div>
  </header>
</template>

<script>
export default {
data(){
    return{
        lists:[],
        input:''
    }
},methods:{
    clearInput(){
    this.input=''
}},
created(){
    fetch('https://www.themealdb.com/api/json/v1/1/categories.php')
    .then(res=> res.json())
    .then(data=>{
      
        this.lists=data.categories.slice(0,3)
    
    })
    .catch(err=>{
        console.log(err);
    })
}
}
</script>

<style>
    .search-div{
        margin: 1.5rem 0;
    }
header{
    padding: 1.5rem 0;
}
.search-div , form{
     height: 2rem;text-align: center;

    margin-inline: auto;
}
form {
    position: relative;
}
.search-input{
    width: 100%;
    height: 100%;
    background-color: rgba(32, 32, 32, 0.829);
    outline: none;
    border: 0;
    color: #eee;
    padding: 0.2rem;
    border-radius: 10px;
}
.search-input:focus{

    background-color: rgba(32, 32, 32, 0.685);

}
.search-input::placeholder{

  color: #eee;

}
.submit{
    position: absolute;
    color: white;
    right: 2px;
    z-index: 10;
    top: 50%;
    transform: translateY(-50%);
}
.option-bar{
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: rgba(32, 32, 32, 0.829);
padding: 0.5rem;
width: 4.2rem;
height: 4.2rem;
border-radius: 50%;
font-size: 14px;
}
.options-div{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1.5rem;
    
}
.router-link-active{
    color: white !important;
    background:linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%) !important;
}
@media screen and (min-width:768px) {
  .search-div , form {
    width: 400px;
    
   
  }  
}
@media screen and (max-width:768px) {
    .search-div, form {
        width: 100%;
        
       
      }  
}
</style>