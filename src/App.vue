<template>
  <div class="wrapper">
    <h1>Погода</h1>
    <p>Узнать погоду в {{ city }}</p>
    <input
        type="text"
        v-model="city"
        placeholder="Введите город"
    >

    <button
        @click="getWeather()"
    >Узнать погоду</button>

    <p class="error">{{ error }}</p>

    <p>{{ info.main }}</p>




  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      city: "",
      error: "",
      info: "null",
    }
  },
  methods: {
    getWeather() {
      if(this.city.trim().length < 2) {
        this.error = "Слишком короткое название"
        return false

      }

      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=c81afc17f0d21b849578798738adeed5`)
          .then(res => (this.info = res.data))
    }
  }
}
</script>

<style>
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: #2d2530;
  padding: 20px;

  text-align: center;
  color: white;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid white;

  color: white;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: #97db97;
  transition: ease all .4s;
}

.wrapper button {
  cursor: pointer;
  padding: 10px 15px;
  background: #97db97;
  border: none;
  border-radius: 10px;
}

.wrapper button:disabled {
  background: white;

}

.error {
  color: red;
}
</style>
