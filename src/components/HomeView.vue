<template>
  <div>
    <select v-model="selectedChartType" @change="updateChartConfig">
      <option value="line">Line</option>
      <option value="bar">Bar</option>
      <option value="column">Column</option>
      <option value="pie">Pie</option>
      <option value="donut">Donut</option>
      <option value="mixed-bar">Mixed (Bar)</option>
      <option value="mixed-pie">Mixed (Pie)</option>
    </select>
    <custom-chart :config="config" />
    <v-jsoneditor v-if="config" v-model="config" height="300px" />
  </div>
</template>

<script>
import CustomChart from './CustomChart.vue'
import json from '../data/charts.json'
import VJsoneditor from 'v-jsoneditor/src/index'

export default {
  components: { CustomChart, VJsoneditor },
  name: 'HomeView',
  data() {
    return {
      config: null,
      selectedChartType: 'line',
      configJson: json
    }
  },
  mounted() {
    this.config = this.configJson[this.selectedChartType];
  },
  methods: {
    updateChartConfig(e) {
      const chartType = e.target.value;
      this.config = this.configJson[chartType];
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
