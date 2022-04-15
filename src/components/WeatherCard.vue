<template>
  <v-container>
    <PageHeader>Weather Forecast</PageHeader>
    <v-card>
      <v-card-title>Weather in Cluj</v-card-title>

      <v-list-item class="text-body-1 font-weight-bold">
        <v-list-item-icon>
          <v-icon>mdi-thermometer</v-icon>
        </v-list-item-icon>
        {{ minTemperatureToday }} - {{ maxTemperatureToday }}</v-list-item
      >
      <v-list-item class="text-body-1 font-weight-bold">
        <v-list-item-icon>
          <v-icon>mdi-weather-pouring</v-icon>
        </v-list-item-icon>
        {{ precipitationToday }}</v-list-item
      >
    </v-card>
  </v-container>
</template>

<script>
import PageHeader from "@/components/PageHeader.vue";

export default {
  name: "WeatherCard",

  components: {
    PageHeader,
  },

  data: () => ({
    forecast: {
      // daily: {
      //   temperature_2m_min: [2.7, 6.4, 3, -1.6, -0.7, 0.4, 5.7],
      //   precipitation_sum: [0, 1.43, 1.1, 0.12, 0.24, 0.03, 0],
      //   temperature_2m_max: [20.6, 13.5, 8.6, 8.3, 10.6, 18.6, 20.6],
      // },
    },
  }),

  async created() {
    const response = await fetch(
      "https://api.open-meteo.com/v1/forecast?latitude=46.77&longitude=23.60&daily=temperature_2m_max,temperature_2m_min,precipitation_sum&timezone=Europe%2FBerlin"
    );
    const result = await response.json();
    this.forecast = result;
  },

  methods: {},

  computed: {
    minTemperatureToday() {
      return this.forecast.daily?.temperature_2m_min[0];
    },
    maxTemperatureToday() {
      return this.forecast.daily?.temperature_2m_max[0];
    },
    precipitationToday() {
      return this.forecast.daily?.precipitation_sum[0];
    },
  },
};
</script>

<style>
</style>
