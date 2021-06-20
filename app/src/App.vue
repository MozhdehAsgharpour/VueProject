<template>
<div class="d-flex justify-content-center"> 
<div class="card" style="width: 18rem;">
  <img src="./assets/1.jpg" class="card-img-top" alt="...">
  <div class="card-body">
    <div class="input-group mb-3">
    <button class="btn btn-primary" type="button" id="button-addon1" @click="getData">ارسال</button>
    <input type="text" class="form-control" placeholder="اسم شهر را وارد کنید" v-model="city" aria-label="Example text with button addon" aria-describedby="button-addon1">
    </div>
    <div class="card-text" v-if="isLoading" >
    <p> اسم شهر: {{data.name}}</p>
    <p> دما : {{data.main.temp}}</p>
    <p> توضیحات : {{data.weather[0].description}}</p>
    <p> سرعت باد: {{data.wind.speed}}</p>
    
    </div>
  
 </div>
</div>
</div>
</template>

<script>
import axios from 'axios'
import HelloWorld from './components/HelloWorld.vue'

const API_KEY = 'c9b269efe8ec42720967207abe54760e';
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data :() =>({
    city:'',
    data:{},
    isLoading:false
    }),
  methods: {
   async getData(){
     this.isLoading = true
     try{  
       const data = await axios.get(`https://api.openweathermap.org/data/2.5/weather`,{
       params:{
          q:this.city,
          appid: API_KEY,
          units:'metric',
          lang: 'fa'
       }
     }).then(({data}) => {
       this.data = data
    })}
     catch(error){
      console.log(error)
     }
 
    }
  },
}
</script>

<style lang="scss">

</style>
