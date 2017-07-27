<template>
  <div>
    <i v-for="star in total" 
      class="star-chart__star fa fa-star"
      v-bind:style="{ color: hex(total) }"
      v-on:mouseenter="mouseEnter"
      v-on:mouseleave="mouseLeave">
    </i>
  </div>
</template>

<script>
  export default {
    'name': 'star-chart-cell',

    props: {
      stars: {
        required: true
      },
      color: ''
    },

    data () {
      return {
        colors: ['#E70D0D', '#E7590D', '#F5ED0F', '#ADE70D', '#13EB13'],
        colorIndex: ''
      }
    },

    created: function () {
      this.colorIndex = this.color
    },

    methods: {
      hex: function (int) {
        var index = int

        if (this.colorIndex !== undefined) index = this.color

        var result = this.colors[index - 1]
        return result
      },

      mouseEnter: function () { this.$emit('mouse-enter') },
      mouseLeave: function () { this.$emit('mouse-leave') }
    },

    computed: {
      total: function () {
        var result = Math.floor(this.stars)
        return result
      }
    }
  }
</script>

<style lang="scss">
  .star-chart {
    &__star {
      margin: 0 2px;
    }
  }
</style>
