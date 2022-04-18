<template>
    <div class="container">
       <div class="row">
           <div class="col-md-8 mx-auto">
               <h3 class="text-white fw-bold">Weather Application</h3>

                 <div>
                      <div class="my-3">
                   <input v-model="query" @keypress.enter="fetchWeather()" class="form-control search-input" type="text" placeholder="Search...">
                   </div>
                 </div>

                    <div>
                       <div class="location" v-if="weather.sys">
                      <div class="location-country">{{ weather.name }},{{ weather.sys.country }}</div>
                      </div>

                      <div class="my-3">
                      <h3 class="date">Monday 20 January 2020</h3>
                      </div>
                   

                     <div class="weather mt-4">
                        <div class="degree-con" v-if="weather.main">
                          <h2 class="degree">{{ Math.round(weather.main.temp) }}°c</h2>
                        </div>
                        <div class="cd-con mt-4"  v-if="weather.main">
                          <h3 class="weather-condition">{{ weather.weather[0].main }}</h3>
                        </div>
                   </div>

                  </div>
           </div>
       </div>
    </div>
</template>

<script>
import { ref } from "vue"

    export default {
        setup(){
            let query=ref("");
            let api_key=ref('45b0f4a65d8fcd3ce7f1d3eb00e6426e');
            let url_base=ref('https://api.openweathermap.org/data/2.5/');
            let weather=ref({});
            
            let fetchWeather=()=>{    
                  fetch(`${url_base.value}weather?q=${query.value}&units=metric&APPID=${api_key.value}`)
                  .then(res=>{
                      return res.json();
                  }).then(setResults)
            }
            
            let setResults=(results)=>{
                 weather.value=results;
                 console.log(weather.value)
            }
            return {query,api_key,url_base,weather,fetchWeather,setResults}
        }
    }
</script>

<style>
body{
    background-image: url(../assets/home.jpg);
    background-repeat: no-repeat;
}
.search-input{
    box-shadow: 0 0 16px #4cc9f0;
    padding: 8px;
    outline: none;
    border: none;
}
.location{
    margin-top: 20px;
}
.location-country{
    font-size: 1.6rem;
    font-weight: bolder;
    color: #fff;
    text-shadow: 2px 3px #4cc9f0;
}
.date{
    font-size: 20px;
    font-style: italic;
    color: #fff;
    font-weight: 300;
}
.degree-con{
    width: 220px;
    height: 80px;
    padding: 7px;
    border: 1px solid white;
    border-radius: 15px;
    box-shadow: 3px 4px #000;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #fff;
    opacity: 0.5;
}
.degree{
    font-size: 3.8rem;
    font-weight: bolder;
    letter-spacing: 2px;
    color: #4cc9f0;
    text-shadow: 2px 3px #000;
}
.weather-condition{
    font-size: 2.5rem;
    font-style: italic;
    font-weight: bolder;
    color: #fff;
    text-shadow: 2px 3px #4cc9f0;
}
</style>