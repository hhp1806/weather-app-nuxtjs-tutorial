<template>
  <v-main>
    <v-container>
      <h1 class="display-1 text-center">Weather App</h1>
      <v-col cols="12">
        <v-card color="purple lighten-2" light>
          <v-card-text>
            <v-layout justify-center>
              <v-flex xs4 text-center>
                <h4>Temperature</h4>
                <h1 class="display-1">{{ weather.name }}</h1>
                <img :src="icon" alt="weather icon" />
                <h3>{{ condition }}</h3>
                <p>
                  <span class="display-2"
                    >{{ Math.round(weather.main.temp - 273) }} &#176;C</span
                  >
                </p>
              </v-flex>
              <v-flex xs4 text-center>
                <h4>Wind & Pressure</h4>
                <h3 class="headline">
                  Wind: {{ weather.wind.speed }} m/s (Degrees:
                  {{ weather.wind.deg }}
                  &deg;)
                </h3>
                <h3 class="headline mt-8">
                  Pressure: {{ weather.main.pressure }} hPa
                </h3>
                <h3 class="headline mt-8">
                  Humidity: {{ weather.main.humidity }} %
                </h3>
              </v-flex>
              <v-flex xs4 text-center>
                <h4>Other</h4>
                <h3 class="headline mt-10">
                  Max Temperature:
                  {{ Math.round(weather.main.temp_max - 273) }} &deg;C
                </h3>
                <h3 class="headline mt-10">
                  Min Temperature:
                  {{ Math.round(weather.main.temp_min - 273) }} &deg;C
                </h3>
              </v-flex>
            </v-layout>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12">
        <v-form @submit.prevent="getWeatherInfo">
          <v-text-field v-model="city" label="Type a city" solo></v-text-field>
        </v-form>
      </v-col>
    </v-container>
  </v-main>
</template>

<script>
export default {
  asyncData({ params, $axios }) {
    return $axios
      .$get(
        `http://api.openweathermap.org/data/2.5/weather?q=Hanoi&appid=${process.env.weatherAppId}`
      )
      .then((res) => {
        return { weather: res }
      })
  },
  data() {
    return {
      city: 'Hanoi',
    }
  },
  computed: {
    icon() {
      return this.weather.weather
        ? `https://openweathermap.org/img/wn/${this.weather.weather[0].icon}.png`
        : ''
    },
    condition() {
      return this.weather.weather ? this.weather.weather[0].description : ''
    },
  },
  created() {
    this.getWeatherInfo()
  },
  methods: {
    getWeatherInfo() {
      this.$axios
        .$get(
          `http://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${process.env.weatherAppId}`
        )
        .then((res) => (this.weather = res))
    },
  },
  head() {
    return {
      title: 'Weather App',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Weather App Page',
        },
      ],
      script: [{}],
    }
  },
}
</script>

<style></style>
