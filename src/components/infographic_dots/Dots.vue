<template>
  <div class="dots">

    <dot v-for="n in achieved" 
      :key="n"
      :classes="typeClass">
    </dot>

    <dot v-for="n in target" 
      :key="n"
      :classes="typeClass"
      class="dot--empty">
    </dot>
  </div>
</template>

<script>
  import Dot from './Dot'

  export default {
    name: 'dots',

    components: { Dot },

    props: {
      dots: { required: true },
      type: { required: true },
      options: {
        dotQuota: { default: 10000 }
      }
    },

    data () {
      return {
        dotQuota: 10000
      }
    },

    created () {
      this.dotQuota = this.options.dotQuota
    },

    computed: {
      achieved: function () {
        var result = this.dots.achieved ? Math.floor(this.dots.achieved / this.dotQuota) : 0
        return result
      },

      target: function () {
        var result = this.dots.target ? Math.floor(this.dots.target / this.dotQuota) : 0
        return result
      },

      typeClass: function () {
        return 'dot--' + this.type
      }
    }
  }
</script>

<style lang="scss" scoped>
  .dots {
    display: flex;
    flex-flow: row wrap-reverse;
  }
</style>
