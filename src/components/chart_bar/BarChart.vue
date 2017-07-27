<template>
  <div>
    <div class="bar-chart"></div>
  </div>
</template>

<script>
  import * as d3 from 'd3'
  import json from '../../json/bar-chart.json'

  export default {
    name: 'bar-chart',

    mounted: function () {
      this.renderChart()
    },

    methods: {
      renderChart: function () {
        // variables
        var width = 420
        var height = 200
        var barHeight = 20

        // chart generation
        var data = json

        var totalData = data.length

        var colour = d3.scaleSequential(d3.interpolateCool)
          .domain([0, totalData])

        var scale = d3.scaleLinear()
                      .domain([0, d3.max(data)])
                      .range([0, width])

        var chart = d3.selectAll('.bar-chart')
          .append('svg')
          .attr('width', '100%')
          .attr('height', '100%')
          .attr('viewBox', '0 0 ' + width + ' ' + height)
          .attr('viewport', width + 'x' + height)
          .attr('preserveAspectRatio', 'xMidYMid')

        var bar = chart.selectAll('g')
          .data(data)
          .enter().append('g')
          .attr('transform', function (d, i) { return 'translate(0,' + i * barHeight + ')' })
          .style('fill', function (d, i) { return colour(i) })

        bar.append('rect')
            .attr('width', scale)
            .attr('height', barHeight - 1)
      }
    }
  }
</script>

<style lang="scss">
  @keyframes grow {
    from {
      width: 0
    }
  }

  .bar-chart {
    svg { fill: yellow; }

    rect { animation: grow 2s linear forwards; }
  }
</style>
