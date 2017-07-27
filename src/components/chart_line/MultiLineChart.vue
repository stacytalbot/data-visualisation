<template>
  <div>
    <div class="multiline-chart"></div>
  </div>
</template>

<script>
  import * as d3 from 'd3'
  import tsv from '../../data/multiline.tsv'

  export default {
    name: 'multiline-chart',

    data () {
      return {
        width: 420,
        height: 200,
        margin: 40,
        svg: ''
      }
    },

    mounted: function () {
      this.renderChart()
    },

    methods: {
      renderChart: function () {
        var data = tsv

        var x = d3.scaleLinear().rangeRound([0, this.width])
        var y = d3.scaleLinear().rangeRound([this.height, 0])

        var line = d3.line()
        .curve(d3.curveBasis)
          .x(function (d) { return x(d.date) })
          .y(function (d) { return y(d.quantity) })

        this.createSVG()

        var animals = this.generateColumns(data)

        x.domain(d3.extent(data, function (d) { return d.date }))

        y.domain([
          d3.min(animals, function (c) { return d3.min(c.values, function (d) { return d.quantity }) }),
          d3.max(animals, function (c) { return d3.max(c.values, function (d) { return d.quantity }) })
        ])

        x.domain(d3.extent(data, function (d) { return d.x }))
        y.domain(d3.extent(data, function (d) { return d.y }))

        var chart = svg.append('g')
          .attr('width', width - margin)
          .attr('height', height - margin)
          .attr('transform', 'translate(' + margin + ', ' + margin + ')')

        chart.append('g')
          .attr('transform', 'translate(0, ' + this.height + ')')
          .call(d3.axisBottom(x))
          .append('text')
          .text('Date')
          .attr('class', 'label')
          .attr('transform', 'translate(' + this.width / 2 + ', 30)')

        chart.append('g')
          .call(d3.axisLeft(y))
          .append('text')
          .text('Quantity')
          .attr('class', 'label')
          .attr('transform', 'rotate(-90) translate(' + -this.height / 2 + ', -30)')

        var animal = chart.selectAll('.animal')
          .data(animals)
          .enter().append('g')
          .attr('class', 'animal')

        animal.append('path')
          .attr('class', 'multi-line')
          .attr('d', function (d) { return line(d.values) })
          .style('stroke', 'steelblue')

        animal.append('text')
          .datum(function (d) { return { id: d.id, value: d.values[d.values.length - 1] } })
          .attr('transform', function (d) { return 'translate(' + (x(d.value.date) + 5) + ',' + y(d.value.quantity) + ')' })
          .attr('class', 'line-label')
          .text(function (d) { return d.id })
      },

      createSVG: function () {
        var svg = d3.select('.multiline-chart')
          .append('svg')
          .attr('viewBox', '0 0 ' + (this.width + 100) + ' ' + (this.height + 100))
          .attr('viewport', (this.width + 100) + 'x' + (this.height + 100))
          .attr('preserveAspectRatio', 'xMidYMid')
          .attr('width', '100%')
          .attr('height', '100%')

        this.svg = svg
      },

      parseTime: function () {
        return d3.timeParse('%d/%m/%Y')
      },

      generateColumns: function (data) {
        data.columns.slice(1).map(function (id) {
          return {
            id: id,
            values: data.map(function (d) {
              return { date: d.date, quantity: d[id] }
            })
          }
        })
      }
    }
  }
</script>

<style lang='scss'>
  .multiline {

  }
</style>
