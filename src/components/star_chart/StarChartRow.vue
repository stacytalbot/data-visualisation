<template>
  <div>
    <div class="star-chart__cell star-chart__cell-title">{{ title }}</div>

    <star-chart-cell v-for="cell, key in cells" 
      :key="key" 
      :stars="cell" 
      class="star-chart__cell"
      :class="{ 'star-chart__cell--hide' : isHidden(cell) }"
      >
    </star-chart-cell>
  </div>
</template>

<script>
  import StarChartCell from './StarChartCell'

  export default {
    'name': 'star-chart-row',

    'components': { StarChartCell },

    'props': {
      row: { 'required': true },
      activeColors: { Type: Array }
    },

    data () {
      return {
        title: '',
        cells: ''
      }
    },

    created: function () {
      this.title = this.row.title
      this.cells = this.row.data
    },

    methods: {
      isHidden: function (index) {
        var indexPosition = this.activeColors.indexOf(index)
        return indexPosition === -1
      }
    }
  }
</script>

<style lang="scss">
  $rowHoverColor: darken(#f2f2f2, 3%);
  
  .star-chart {
    &__row {
      background-color: #fafafa;
      padding: 4px;
      text-align: left;

      display: flex;

      &:nth-child(even) { background-color: #f2f2f2; }

      &:hover { 
        background-color: $rowHoverColor; 
        &:nth-child(even) { background-color: $rowHoverColor; }
      }
    }

      &__cell {
        flex: 20%;
        padding: 0 10px;

        &--hide { visibility: hidden; }
      }

      &__cell-title {
        text-align: right;
        text-transform: capitalize;
      }
  }
</style>
