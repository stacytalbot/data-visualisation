<template>
  <div class="star-chart">
    
    <div class="star-chart__column-titles">
      <div v-for="title in columnTitles" class="star-chart__column-title">{{ title }}</div>
    </div>

    <div class="star-chart__rows">
      <star-chart-row v-for="row, i in rows" 
        :row="row" 
        :key="i"
        :activeColors="activeColors"
        class="star-chart__row">
      </star-chart-row>
    </div>

    <div class="star-chart__key">
      Filter by rating
      <star-chart-cell v-for="key, i in keyTotal" 
        stars="1"
        :key="i" 
        :color="i+1"
        class="star-chart__key-item"
        v-on:mouse-enter="mouseEnter(i+1)"
        v-on:mouse-leave="mouseLeave">
      </star-chart-cell>
    </div>
  </div>
</template>

<script>
  import StarChartRow from './StarChartRow'
  import StarChartCell from './StarChartCell'

  export default {
    'name': 'star-chart',

    'components': { StarChartRow, StarChartCell },

    props: {
      json: { required: true }
    },

    data () {
      return {
        columnTitles: {},
        rows: {},
        keyTotal: 5,
        activeColors: [1, 2, 3, 4, 5]
      }
    },

    created: function () {
      this.columnTitles = this.json.columnTitles
      this.rows = this.json.rows
    },

    methods: {
      mouseEnter: function (int) {
        this.activeColors = [int]
      },

      mouseLeave: function () {
        this.activeColors = [1, 2, 3, 4, 5]
      }
    }
  }
</script>

<style lang="scss" scoped>
  .star-chart {
    &__column-titles {
      display: flex;
      font-weight: bold;
      text-align: left;
    }

      &__column-title {
        flex: 20%;
        padding: 0 12px;
        text-transform: capitalize;
      }

    &__key {
      margin: 20px auto;

      display: inline-block;
    }

      &__key-item {
        cursor: pointer;
        margin: 0 10px;
        display: inline;
      }
  }  
</style>
