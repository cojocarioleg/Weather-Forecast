<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: "",
      error: "",
      info: null
    }
  },
  computed: {
    cityName() {
      return ">>" + this.city + "<<"
    },
    showTemp(){
      return "temperature: " + this.info.main.temp;
    },
    showFeelsLike(){
      return "Feels Like: " + this.info.main.feels_like;
    },
    showMinTemp(){
      return "Min Temp: " + this.info.main.temp_min;
    },
    showMaxTemp(){
      return "Max Temp: " +this.info.main.temp_max;
    }

  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "nead more one liter";
        return false;
      }
      this.error="";

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=1b0a70037662f63b0781c2bfeaf35168`)
      .then(res=>(this.info = res.data))
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Weather Forecast </h1>
    <p>Find out the weather forecast in {{ city == "" ? ": Your city" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Enter the name of your city">
    <button v-if="city != ''" @click="getWeather()">weather</button>
    <button disabled v-else>Insert your city</button>
    <p class="error"> {{ error }}</p>
   
    <div v-if="info !=null">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp}}</p>
      <p>{{ showMaxTemp }}</p>
    </div>
    
  </div>
</template>

<style scoped>
  .error {
    color: #d03939;
  }

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff;
}

.wrapper h1 {
  margin-top: 50px;
  text-transform: uppercase;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}

.wrapper button:disabled {}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
  text-transform: uppercase;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}
</style>
