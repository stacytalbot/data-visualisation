<template>
  <div>
    <div class="line-chart"></div>
  </div>
</template>

<script>
  import * as d3 from 'd3'
  import json from '../../json/line-chart.json'

  export default {
    name: 'line-chart',

    mounted: function () {
      this.renderChart()
    },

    methods: {
      renderChart: function () {
        // variables
        var width = 420
        var height = 200
        var margin = 40

        var data = json

        // chart functions
        var x = d3.scaleLinear()
          .rangeRound([0, width])

        var y = d3.scaleLinear()
          .rangeRound([height, 1])

        var line = d3.line()
          .x(function (d) { return x(d.x) })
          .y(function (d) { return y(d.y) })

        // build chart
        var svg = d3.select('.line-chart')
          .append('svg')
          .attr('viewBox', '0 0 ' + (width + 100) + ' ' + (height + 100))
          .attr('viewport', (width + 100) + 'x' + (height + 100))
          .attr('preserveAspectRatio', 'xMidYMid')
          .attr('width', '100%')
          .attr('height', '100%')

        var chart = svg.append('g')
          .attr('width', width - margin)
          .attr('height', height - margin)
          .attr('transform', 'translate(' + margin + ', ' + margin + ')')

        x.domain(d3.extent(data, function (d) { return d.x }))
        y.domain(d3.extent(data, function (d) { return d.y }))

        chart.append('g')
          .attr('transform', 'translate(0, ' + height + ')')
          .call(d3.axisBottom(x))
          .append('text')
          .text('Price (£)')
          .attr('class', 'label')
          .attr('transform', 'translate(' + width / 2 + ', 30)')

        chart.append('g')
          .call(d3.axisLeft(y))
          .append('text')
          .text('Quantity')
          .attr('class', 'label')
          .attr('transform', 'rotate(-90) translate(' + -height / 2 + ', -30)')

        chart.append('path')
          .datum(data)
          .attr('fill', 'none')
          .attr('class', 'line-1')
          .attr('d', line)
      }
    }
  }
</script>

<style lang='scss'>
  .label {
    fill: $grey-medium;
    font-weight: bold;
  }

  .domain {
    stroke: $grey-dark;
  }

  .tick {
    line {
      stroke: $grey-dark; 
    }

    text {
      fill: $grey-dark;
    }
  }

  .line-1 {
    stroke: $green;
    stroke-linejoin: bevel;
  }

  .line-label {
    font-size: 0.4rem;
    text-transform: capitalize;
  }
</style>
