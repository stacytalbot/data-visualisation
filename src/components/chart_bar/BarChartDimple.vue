<template>
  <div class="dimple-bar-chart"></div>
</template>

<script>
  import * as d3 from 'd3'
  import dimple from 'dimple'

  export default {
    name: 'bar-chart-dimple',

    props: {
      json: {}
    },

    data () {
      return {
        width: 420,
        height: 200,
        data: [
          { 'Word': 'Hello', 'Awesomeness': 2000 },
          { 'Word': 'World', 'Awesomeness': 3000 }
        ]
      }
    },

    mounted: function () {
      this.renderChart()
    },

    methods: {
      renderChart: function () {
        console.log('chart')
        var svg = dimple.newSvg('.dimple-bar-chart')
        var chart = new dimple.chart(svg, this.data)

        chart.addCategoryAxis('x', 'Word')
        chart.addMeasureAxis('y', 'Awesomeness')
        chart.addSeries(null, dimple.plot.bar)
        chart.draw()
      },

      createSVG: function () {
        var svg = d3.select('.dimple-bar-chart')
          .append('svg')
          .attr('viewBox', '0 0 ' + this.width + ' ' + this.height)
          .attr('viewport', this.width + 'x' + this.height)
          .attr('preserveAspectRatio', 'xMidYMid')
          .attr('width', '100%')
          .attr('height', '100%')

        return svg
      }
    }
  }
</script>

<style lang="scss">
  
</style>
