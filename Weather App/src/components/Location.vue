<template>
    <div class="input-group">
      <label>Input Location: </label>
      <input type="text" v-model="location" />
      <button @click="handleSubmit">Submit Location</button>
    </div>

</template>



<script>

export default {
    data(){
        return{
            location: '',
        };
    },

    methods: {
        async handleSubmit() {
            if (!this.location){
                 alert("Input Location!") //if there is no location input
                return;
            }
            
            else{
                const apiKey = import.meta.env.VITE_API_KEY;
                const apiUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${this.location}&appid=${apiKey}`;
                
                const response = await fetch(apiUrl);
                const data = await response.json();

                console.log(response);

                if (!response.ok){
                    alert ("Location entered does not exist, please enter a real location")
                    throw new Error("Couldn't fetch weather data");
                }
                
                this.$emit('weather-data', data);
            /*
                try{
                    const weatherData = await this.getWeatherData(this.location);
                    this.displayWeatherData(weatherData);
                }
                catch(error){
                    //console.error(error);
                    this.errorSpotted(error.message);
                };*/
            }
        }

    }
}

</script>


<style scoped>
  .input-group{
    height: 90px;
    width: 200px;
    background-color: aqua;
    text-align: center;
    margin-left: 450px;
    margin-top: 330px;
  }
</style>