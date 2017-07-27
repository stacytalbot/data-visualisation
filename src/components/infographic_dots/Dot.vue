<template>
  <div class="dot" :class="classes"></div>
</template>

<script>
  export default {
    name: 'dot',

    props: { classes: { required: true } }
  }
</script>

<style lang="scss">
  $dotSize: 60%;
  $dotsPerRow: 5;
  $marineColor: #2B9DDE;
  $terrestrialColor: #17e855;

  @keyframes animate {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  
  .dot {
    $flexBasis: 100 / $dotsPerRow + %;

    flex: 0 1 $flexBasis;
    opacity: 0;

    animation: animate .5s 1 forwards ease-out;

    &:before {
      border: solid 2px black;
      border-radius: 100px;
      content: "";
      display: block;
      margin: 14.5% auto;
      padding-top: $dotSize;
      width: $dotSize;
    }

    &--terrestrial:before { 
      border-color: $terrestrialColor;
      background-color: $terrestrialColor;
    }

    &--marine:before { 
      border-color: $marineColor;
      background-color: $marineColor; 
    }

    &--empty:before { background-color: transparent; }

    &--tooltip {
      opacity: 1;
      vertical-align: bottom;
      width: 20px;

      display: inline-block;

      animation: none;
    }
  }

  @for $i from 1 through 100 {
    .dot:nth-child(#{$i}) {
      animation-delay: .1s * ($i/$dotsPerRow); 
    }
  }
</style>
