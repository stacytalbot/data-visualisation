<template>
  <div class="site-width">
    <h1>Marine Data Manual Ideas</h1>
    
    <h2>Star chart</h2>

    <star-chart :json="jsonStar"></star-chart>

    <h2>Sunburst chart</h2>

    <sun-burst-chart :json="jsonSunBurst"></sun-burst-chart>
    <!-- <sunburst :json="jsonSunBurst"></sunburst> -->
  </div>
</template>

<script>
  import dataStar from './data/marine-star-chart.csv'
  import StarChart from './components/star_chart/StarChart'
  import dataSunBurst from './data/marine-sun-burst-chart.json'
  import SunBurstChart from './components/chart_sun_burst/SunBurstChart'
  import Sunburst from './components/chart_sun_burst/Sunburst'

  export default {
    'name': 'marine-data-manual',

    'components': { StarChart, SunBurstChart, Sunburst },

    data () {
      return {
        jsonStar: {},
        jsonSunBurst: {}
      }
    },

    created: function () {
      this.jsonStar = this.refactorJson(dataStar)
      this.jsonSunBurst = dataSunBurst
    },

    methods: {
      refactorJson (data) {
        var json = {}
        var rows = []
        var columnTitles = []

        // loop thorough data and create an array of rows for the start chart
        for (let dataObject of data) {
          var dataValues = []
          var row = {}

          for (let column of data.columns) {
            if (column !== 'id') {
              let dataValue = dataObject[column]
              dataValues.push(parseInt(dataValue))
            }
          }

          row.title = dataObject.id
          row.data = dataValues

          rows.push(row)
        }

        // loop thorough data.columns and create an array of column title for the star chart
        // ignore the first one
        for (let column of data.columns) {
          if (column === 'id') {
            columnTitles.push('')
          } else {
            columnTitles.push(column)
          }
        }

        // assign arrays to the json object and return
        json.columnTitles = columnTitles
        json.rows = rows

        return json
      }
    }
  }
</script>

<style lang="scss" scoped>
  
</style>
