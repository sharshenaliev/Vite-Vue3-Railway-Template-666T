<script >
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
    showTemp() {
      return "Temperature:" + this.info.main.temp
    },
    showPres() {
      return "Pressure:" + this.info.main.pressure
    },
    showHum() {
      return "Humidity:" + this.info.main.humidity
    }
  },
  methods: {
    getWeather() {
      if(this.city.trim().length < 2) {
        this.error = "Should have more than 2 letters" 
        return false
      }

      this.error = ""
      
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=4d7eae943b5e49b7962feaf80b0817d5`)
          .then(res => (this.info = res.data))
    }
  }
}
</script>

<template>
    <div class="container">
      <div class="p-[10%]">
        <div class="min-w-full w-full h-96 bg-white border border-gray-200 rounded-3xl shadow dark:bg-gray-800 dark:border-gray-700">
          <h5 class="m-2 text-2xl text-center font-bold tracking-tight text-gray-900 dark:text-white">Weather app</h5>
          <p class="m-3 text-center font-normal text-gray-700 dark:text-gray-400">
            Check the weather in {{ city == '' ? 'your city': city }}
          </p>
          <div class="pl-[5%] flex justify-center grid grid-cols-1">
            <div class="grid grid-cols-2 gap-3">
              <input type="text" v-model="city" placeholder="input city" class="m-3 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              <button v-if="city != ''" @click="getWeather()" class="inline-flex items-center m-3 p-3 w-3/4 text-sm font-medium text-center text-white bg-blue-700 rounded-lg">
                Get
                <svg aria-hidden="true" class="w-4 h-4 ml-2 -mr-1" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
              </button>
              <button disabled v-else class="inline-flex items-center m-3 p-3 w-3/4 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                Input
                <svg aria-hidden="true" class="w-4 h-4 ml-2 -mr-1" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
              </button>
              <p class="m-3 text-center font-normal text-gray-700 dark:text-gray-400">{{ error }}</p>
            </div>
            <div v-if="info != null">
                <p class="m-3 text-center font-normal text-gray-700 dark:text-gray-400">{{ showTemp }}</p>
                <p class="m-3 text-center font-normal text-gray-700 dark:text-gray-400">{{ showPres }}</p>
                <p class="m-3 text-center font-normal text-gray-700 dark:text-gray-400">{{ showHum }}</p>
              </div>
          </div>
        </div>
      </div>
    </div>
</template>

<style scoped>

</style>