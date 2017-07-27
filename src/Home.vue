<template>
  <div class="site-width">
    <h1>Marine PA Ideas</h1>
    
    <h2>Bar Chart</h2>
    <bar-chart-dimple :json="jsonBar"></bar-chart-dimple>
    <bar-chart></bar-chart>

    <h2>Line Chart</h2>
    <line-chart></line-chart>
    <!-- <multiline-chart class="line-chart--fancy"></multiline-chart> -->
    
    <h2>Infographic - Brian</h2>
    <infographic :json="json"></infographic>
    <!-- <infographic :json="json2"></infographic> -->

    <h2>Wave</h2>
    <wave-infographic></wave-infographic>
  </div>
</template>

<script>
  import BarChart from './components/chart_bar/BarChart'
  import BarChartDimple from './components/chart_bar/BarChartDimple'
  import LineChart from './components/chart_line/LineChart'
  import MultilineChart from './components/chart_line/MultilineChart'
  import Infographic from './components/infographic_dots/Infographic'
  import WaveInfographic from './components/infographic_wave/WaveInfographic'

  import json from './json/marine-dot.json'
  import json2 from './json/marine-dot-2.json'
  import jsonBar from './json/bar-chart.json'

  export default {

    'name': 'home',

    components: {
      Infographic,
      BarChart,
      BarChartDimple,
      LineChart,
      MultilineChart,
      WaveInfographic
    },

    data () {
      return {
        json: {},
        json2: {},
        jsonBar: {}
      }
    },

    created: function () {
      this.json = json
      this.json2 = json2
      this.jsonBar = jsonBar
    }
  }

</script>
