<template>
  <div style="background: #DDDDDD; padding: 1rem 3rem" class="container">
    <main>
      <div class="search-box">
        <input type="text" v-model="city" class="form-control" placeholder="City">
        <button @click="getWeather()" type="button" class="btn">Find</button>
        <div v-if="(typeof weather.main) != 'undefined'"> 
          <p>
            City: {{ weather.name }}, {{ weather.sys.country }}
          </p>
          <p style="color: ">
            Degree: {{ Math.round(weather.main.temp) }}
          </p>
        </div>
        <h1 v-if="(typeof weather) != 'undefined'" > 
          {{ weather.sys.country }}
        </h1>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      api_key: '240c641251721b924b1f8e5d425057a6',
      city: 'Tashkent',
      units: 'metric',
      weather: {}
    }
  },
  methods: {
    async getWeather() {
      await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.api_key}&units=${this.units}`)
        .then(res => {
          return res.json()
        }).then(this.setResults)
    },
    setResults(results) {
      this.weather = results
      
      console.log(this.weather)
    }
  }
}
</script>

<style>

</style>
