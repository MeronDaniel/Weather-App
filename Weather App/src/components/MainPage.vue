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

<template>
  <div class="page-wrapper">


    <form class="input-group">
      <label>Input Location: </label>
      <input type="text" v-model="location" />
      <button type="submit">Submit Location</button>
    </form>
  </div>

  <div class="presentFuture">
      <div class="currentTemp"> <p>Current Temperature: </p>
          <input type="text" id="currTemp" readonly="currTemp">
      </div>

      <div class="emoji"> <p>Weather Emoji: </p>
          <input type="text" id="emo" readonly="emo">
      </div>

      <div class="feelsLike"> <p>Feels Like: </p>
          <input type="text" id="feeLik" readonly="feeLik">
      </div>
  </div>


  <div class="elements">
    <div class="humidity"> <p>Humidity: </p>
        <input type="text" id="humid" readonly>
    </div>

    <div class="wind"> <p>Wind: </p>
        <input type="text" id="wind" readonly="wind">
    </div>

    <div class="precipitation"> <p>Precipitation: </p>
        <input type="text" id="precip" readonly="precip">
    </div>
  </div>
  


  <!--<div class="greetings">

  </div>-->
</template>



<script>
export default {
  data() {
    return {
      location: ''
    }
  },
  /*methods: {
    async handleRegister() {
      try {
        // Validate inputs
        if (!this.email || !this.password || !this.confirmPassword) {
          alert('Please fill in all fields')
          return
        }

        if (this.password !== this.confirmPassword) {
          alert('Passwords do not match')
          return
        }

        this.isLoading = true

        // Make API call to register
        const response = await fetch('http://localhost:3000/api/auth/register', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            email: this.email,
            password: this.password
          })
        })

        const data = await response.json()

        if (!response.ok) {
          throw new Error(data.message || 'Registration failed')
        }

        // Registration successful
        alert('Account created successfully! Please log in.')
        this.$router.push('/login')
      } catch (error) {
        alert(error.message || 'Failed to create account. Please try again.')
        console.error('Registration error:', error)
      } finally {
        this.isLoading = false
      }
    }
  }*/
}
</script>



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
