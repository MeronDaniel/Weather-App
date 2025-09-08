<!--<script setup lang="ts">
import { loadEnv } from 'vite';

</script>-->

<!--Originally called HelloWorld.vue-->

<!--<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
})
</script>-->*/

<script>
import Location from "./Location.vue";

export default {
  components: {
    Location,
  },
  data() {
    return {
      currTemp: '',
      feeLik: '',
      humid: '',
      wind: '',
      precip: '',
      emo: ''
    }
  },

  methods: {
    displayWeatherData(data){

      const {name: location, 
          main: {temp, humidity, feels_like, sea_level},
          weather: [{description, id}],
          wind: {speed}} = data.list[0];
      
      this.currTemp = `${(temp - 273.15).toFixed(1)}°C`;
      //console.log(this.currTemp);
      //console.log(currTemp);

      this.feeLik = `${(feels_like - 273.15).toFixed(1)}°C`;

      this.humid = `${humidity}%`

      this.wind = `${speed * 3.6} km/h`; //wind default measurement is metres/second
      
      this.precip = `${sea_level}%`;

      this.emo = this.getWeatherEmoji(id);
    },

    getWeatherEmoji(weatherID){
      switch(true){

        case(weatherID >= 200 && weatherID <= 232):
            return "⛈️";
        
        case(weatherID >= 300 && weatherID <= 321):
            return "🌦";
        
        case(weatherID >= 500 && weatherID <= 531):
            return "🌧️";
        
        case(weatherID >= 600 && weatherID <= 622):
            return "❄️";
        
        case(weatherID >= 701 && weatherID <= 781):
            return "🌫️";
        
        case(weatherID === 800):
            return "☀️";
        
        case(weatherID >= 801 && weatherID <= 804):
            return "☁️";

        default:
            return "NOTHING"; 
      }
    }
  }



}
</script>

<template>
  <div class="page-wrapper">
    <Location @weather-data="displayWeatherData" />
  </div>

  <div class="presentFuture">
      <div class="currentTemp"> <p>Current Temperature: </p>
          <input type="text" :value="currTemp" readonly>
      </div>

      <div class="emoji"> <p>Weather Emoji: </p>
          <input type="text" :value="emo" readonly>
      </div>

      <div class="feelsLike"> <p>Feels Like: </p>
          <input type="text" :value="feeLik" readonly>
      </div>
  </div>


  <div class="elements">
    <div class="humidity"> <p>Humidity: </p>
        <input type="text" :value="humid" readonly>
    </div>

    <div class="wind"> <p>Wind: </p>
        <input type="text" :value="wind" readonly>
    </div>

    <div class="precipitation"> <p>Precipitation: </p>
        <input type="text" :value="precip" readonly>
    </div>
  </div>
  

</template>







<style scoped>

  .page-wrapper {
    display: flex;
    padding-top: 60px;
  }


  .input-group{
    height: 90px;
    width: 200px;
    background-color: aqua;
    text-align: center;
    margin-left: 450px;
    margin-top: 330px;
  }
  
  .presentFuture{
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    margin-bottom: 320px;
  }

  .currentTemp, .emoji, .feelsLike{
      height: 200px;
      width: 300px;
      font-weight: bold;
      text-align: center;
      background-color: aqua;
      border: 1px solid blue;
      border-radius: 30%;
      margin-top: 190px;
      margin-right: 50px;
  }


  .elements {
      display: flex;
      flex-direction: row;
      justify-content: flex-end;
      margin-bottom: 50px;
  }

  .humidity, .wind, .precipitation {
      height: 200px;
      width: 300px;
      font-weight: bold;
      text-align: center;
      background-color: aqua;
      border: 1px solid blue;
      border-radius: 30%;
      /*margin-bottom: 1000px; pushes the blue background furthur down NOT the 3 text boxes*/
      margin-right: 100px;
  }


/*
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}*/


</style>
