<script setup lang="ts">
  import { Bar } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
</script>

<template>
  <Bar
    v-if="loaded"
    id="energychart"
    :data="chartData"
  />
</template>

<script lang="ts">
  ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

  export default {
    name: 'BarChart',
    components: { Bar },
    data: () => ({
        chartData: null
    }),
    methods: {
      async getData() {
        const res = await fetch("http://localhost:8000/metrics/month?start=2023-04-01");
        const finalRes = await res.json();
        this.chartData = finalRes;
      }
    },
    mounted() {
      this.getData()
    }
  }
</script>