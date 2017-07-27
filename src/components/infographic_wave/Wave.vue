<template>
  <div class="wave">
    <div class="wave__circle">
      <div 
        class="wave__animated"
        :style="{ top: top }">
      </div>

      <span class="wave__number">{{ percentage }}%</span>
    </div>  
    <p class="wave__title">{{ name }}</p>
  </div>
</template>

<script>
  export default {
    name: 'wave',

    props: {
      name: '',
      percentage: 0
    },

    computed: {
      top: function () {
        return 100 - this.percentage + '%'
      }
    }
  }
</script>

<style lang="scss">
  @mixin animation-delay {
    animation-delay: random(4) + s;
  }

  @keyframes spin {
    100% { transform: rotate(360deg); }
  }

  .wave {

    &:nth-child() .wave__animated {
      background-color: red;
      @include animation-delay();
    }

    &__circle {
      border: solid 5px #1fb3d3;
      border-radius: 100%;
      margin: 0 auto;
      overflow: hidden;
      width: 200px; height: 200px;
      position: relative;
    }

    &__animated {
      background-color: #1fb3d3;
      border-radius: 38% 42%;
      box-shadow: inset 0 0 50px rgba(255,255,255,0.8);
      margin-left: -100%;
      width: 200%; height: 200%;
      
      position: absolute;
      top: 50%;
      left: 50%;
      
      animation: spin 14s infinite linear; 
    }

    &__number {
      font-size: 60px;

      position: absolute;
      top: 50%;
      left: 50%;

      transform: translate(-50%, -50%);
    }
    
    &__title {
      font-size: 20px;
      font-weight: bold;
      text-transform: capitalize;
    }
  }  

  @for $i from 1 through 100 {
    .wave:nth-child(#{$i}) .wave__animated {
      animation-delay: -.1s * ($i) * random(10); 
    }
  }
</style>
