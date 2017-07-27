<template>
  <div class="waves">
    <wave v-for="wave in waves" 
      :name="wave.name" 
      :percentage="wave.percentage"
      class="waves__wave">
    </wave>
  </div>
</template>

<script>
  import Wave from './Wave'
  import json from '../../data/wave.json'

  export default {
    name: 'wave-infographic',

    components: { Wave },

    data () {
      return {
        waves: {}
      }
    },

    created: function () {
      this.waves = json
    }
  }
</script>

<style lang="scss">
  .waves {
    display: flex;

    &__wave {
      flex: 0 0 20%;
    }
  }
</style>
