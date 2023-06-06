<script>
import axios from 'axios';

const weekDay = new Date();

export default {
  data() {
    return {
      info: {},
      time: '',
      inputValue: ''
    }
  },
  created(){
    this.request()
    this.realTime()
  },
  methods: {
    async request(){
      let city = this.inputValue;
      if (city === '') {
        city = 'Buenos_Aires'; // 
      }
      const URL_BASE = `https://api.weatherapi.com/v1/current.json?key=7fced194b00043a6bba184433230106&q=${city}`;
      try {
        this.info =  await (await axios(URL_BASE)).data
        this.time = weekDay
        
      } catch (error) {
        alert('City not found')
      }
    },
    mounted() {
      this.request(); 
    },
    realTime(day){
      if(day === 0) return 'Sunday';
      if(day === 1) return 'Monday';
      if(day === 2) return 'Tuesday';
      if(day === 3) return 'Wednesday';
      if(day === 4) return 'Thursday';
      if(day === 5) return 'Friday';
      if(day === 6) return 'Saturday';
    },
    handleInput(event){
      const { value } = event.target;
      this.inputValue = value;
    }
  }
}
</script>



<template>
  <main class="container">
    <div class="city_info">
      <h1>{{ info.location?.name }}</h1>
      <h3>{{ info.location?.region }}, {{ info.location?.country }}</h3>
    </div>
    <div class="wheather_time">
      <div class="weather_info">
        <div class="img_temp">
          <img class="imagen" :src='info.current?.condition?.icon' alt="icon">
          <h3>{{ info.current?.temp_c }}°</h3>
        </div>
        <div class="details">
          <h5>Feels like: {{ info.current?.feelslike_c }}°</h5>
          <h5>Humidity: {{ info.current?.humidity }}%</h5>
          <h5>Wind: {{ info.current?.wind_kph }}km/h</h5>
        </div>
      </div>
    </div>
    <div class="time_info">
      <h5>{{ realTime(time.getDay()) }}, {{ info.location?.localtime?.slice(11,16) }}</h5>
      <h5>{{ info.current?.condition?.text }}</h5>
      <h5>UV Index: {{ info.current?.uv }}</h5>

      <input class="cityInput" type="text" v-on:input="handleInput" placeholder="City">
      <button class="btn_city" @click="request" >Select</button>
    </div>
  </main>
</template>


<style>
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  border-left: 2px solid rgba(253, 242, 242, 0.986);
  padding: 10px 0px;
  background-color: rgba(255, 255, 255, 0.8);
  padding: 10px;
  border-radius: 0px 10px 10px 0px;
}

.city_info {
  margin: 5px 0px;
}

.weather_info {
  display: flex;
  justify-content: flex-start;
  width: 250px;
  margin: 10px 0px;
}

.img_temp {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 15px;
  border-right: 2px solid rgba(8, 29, 121, 0.342);
  padding-right: 5px;
}

.img_temp h3 {
  font-weight: bold;
}

.imagen {
  width: 60px;
  height: 60px;
}

.weather_info h2 {
  font-size: 40px;
}

.weather_info img {
  display: inline-flex;
  font-size: 40px;
  align-items: center;
}

.wheather_time {
  margin: 5px 0px;
  font-size: large;
}

.time_info {
  margin: 5px 0px;
  font-size: large;
}

.time_info h5 {
  font-weight: bolder;
}

.cityInput {
  border: none;
  height: 30px;
  line-height: 30px;
  border-radius: 3px;
  margin: 5px 5px;
  border: 2px solid transparent;
}

.cityInput:focus {
  border: 2px solid #222222;
}

.btn_city {
  border: none;
  background: #222222;
  color: #fff;
  height: 30px;
  width: 60px;
  border-radius: 3px;
  cursor: pointer;
}

</style>