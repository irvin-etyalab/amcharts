<template>
  <div style="padding: 24px">
    <div ref="chartdiv" id="chartDiv" />
  </div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

export default {
  name: "CustomChart",
  data() {
    return {
      chart: null,
    }
  },
  props: {
    config: Object,
  },
  watch: { 
    config: function(newVal, oldVal) {
      console.log('Prop changed: ', newVal, ' | was: ', oldVal)
      this.createChart();
    }
  },
  mounted() {
    am4core.useTheme(am4themes_animated);
  },
  methods: {
    createChart() {
      if (this.chart) {
        this.chart.dispose();
      }

      if(this.config !== null) {
        this.chart = am4core.createFromConfig(this.config, this.$refs.chartdiv, am4charts[this.config.type]);
      }
    }
  },
}
</script>

<style scoped>
  #chartDiv {
    width: 100%;
    height: 400px;
  }
</style>