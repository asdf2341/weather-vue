<script>
import axios from 'axios'
export default {
  data(){
    return {
    city:"",
    error:"",
    info:null

    }
  },
  computed:{
    cityName(){
      return "'"+this.city+"'"
    },
    showTemp(){
      return "Temperature:"+this.info.main.temp+" °C"
    },
    showFeelsLIke(){
      return "Feels like:"+this.info.main.feels_like+" °C"
    },
    showMinTemp(){
      return "Min temp:"+this.info.main.temp_min+" °C"
    },
    showMaxTemp(){
      return "Max temp:"+this.info.main.temp_max+" °C"
    }

}  ,
  methods:{
    getWeather(){
      if(this.city.trim().length<2){
        this.error="You need to write more than one letter!"
        return false
      }
      this.error=""
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=b1145dc706066b3401e389537c7121a6`)
        .then(res=>(this.info=res.data))
    }
  }
}
  
  
  

</script>

<template>
 
<div class="wrapper">
  <h1>Weather app</h1>
  <p className="describe">Check the weather in {{ city=="" ? "in your city" : cityName}}</p>
  <input type="text" v-model="city" placeholder="Enter city">
  <button type="button" v-if="city!=''" @click="getWeather()">Get the weather</button>
  <button disabled  v-else>Enter the name of city!</button>
  <p className="error">{{ error }}</p>
  <div className="info" v-if="info!=null">
  
    <p>{{ showTemp }}</p>
    <p>{{ showFeelsLIke }}</p>
    <p>{{ showMinTemp }}</p>
    <p>{{ showMaxTemp }}</p>

  </div>

</div>

</template>

<style scoped>
.info{
  border-radius: 10px;
background-color: #833AB4;
  margin:2rem 20rem;
  text-align: left;
}
.info p{
  padding:8px 10px;
  font-size: 25px;
}

.error{
  margin-top:10px;
  color:#d03939;
}
.wrapper{
  width:900px;
  height:500px;
  border-radius: 50px;
  padding:20px;
  background: #050538;
  text-align: center;
  color:#fff;
  margin:50px 0;
}
.wrapper h1{
  margin-top:50px;

}
.describe{
  margin-top: 20px;
  font-size: 25px;
}
.wrapper button:disabled{
  background-color: rgb(128, 27, 27);
  cursor: not-allowed;
  border:none;
  outline:none
}
.wrapper button{
  background-color: #FF7BA9;
  color:#fff;
  border-radius: 10px;
  border:2px solid silver;
  padding:10px 15px;
  margin-top:30px;
  margin-left:20px;
  font-size: 20px;
  outline:none;
  cursor:pointer;
  transition:transform 500ms ease;
}
.wrapper button:hover{
  transform:scale(1.1) translateY(-5px)
}
.wrapper input{
  margin-top:30px;
  background: transparent;
  border: none;
  border-bottom:2px solid  #FFC857 ;
  color:#fcfcfc;
  font-size:20px;
  padding:5px 8px;
  outline:none;
  width:200px;
}
/* .wrapper input:focus{
  border-bottom-color:#110813;
} */
</style>
