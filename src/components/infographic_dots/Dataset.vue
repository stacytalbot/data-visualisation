<template>
  <div class="dataset">

    <div class="dataset__tooltip tooltip" v-show="toolTipActive">
      <h3>Protected Areas</h3>
      
      <div class="tooltip__section tooltip--marine">
        <h4>Marine</h4>
        <h5 class="marine"><dot classes="dot--marine dot--empty dot--tooltip"></dot> Target</h5>
        <span class="total">{{ categories.marine.target || 0 }} km<sup>2</sup></span>
        
        <h5 class="marine"><dot classes="dot--marine dot--tooltip"></dot> Achieved</h5>
        <span class="total">{{ categories.marine.achieved || 0 }} km<sup>2</sup></span>
      </div>
      
      <div class="tooltip__section tooltip--terrestrial">
        <h4>Terrestrial</h4>
        <h5 class="terrestrial"><dot classes="dot--terrestrial dot--empty dot--tooltip"></dot> Target</h5>
        <span class="total">{{ categories.terrestrial.target || 0 }} km<sup>2</sup></span>
        
        <h5 class="terrestrial"><dot classes="dot--terrestrial dot--tooltip"></dot> Achieved</h5>
        <span class="total">{{ categories.terrestrial.achieved || 0 }} km<sup>2</sup></span>
      </div>
    </div>
    
    <dots 
      :dots="categories.marine" 
      :options="options"
      type="marine">
    </dots>

    <dots 
      :dots="categories.terrestrial" 
      :options="options"
      type="terrestrial">
    </dots>

    <p class="dataset__title" v-on:mouseenter="mouseEnter" v-on:mouseleave="mouseLeave">
      {{ title }} <span class="dataset__i">i</span>
    </p>

    <p class="dataset__year"><strong>{{ year }}</strong></p>
  </div>
</template>

<script>
  import Dots from './Dots'
  import Dot from './Dot'

  export default {
    name: 'datset',

    components: { Dots, Dot },

    props: {
      title: { required: true },
      year: { required: true },
      categories: { required: true },
      options: {}
    },

    data () {
      return {
        toolTipActive: false
      }
    },

    methods: {
      mouseEnter: function () {
        this.toolTipActive = true
      },

      mouseLeave: function () {
        this.toolTipActive = false
      }
    }
  }
</script>

<style lang="scss" scoped>
  $tooltipPadding: 16px;
  $marineColor: #2B9DDE;
  $terrestrialColor: #17e855;
  $marineColorBg: #d6effc;
  $terrestrialColorBg: #def9e6;

  .dataset {
    flex: 0 1 22%;

    position: relative;

    &__title { 
      cursor: pointer;
      margin-bottom: 0; 
    }

    &__year { margin-top: 4px; }

    &__tooltip {
      background-color: white;
      text-align: left;

      position: absolute;
      right: 2px;
      bottom: 85px;
      left: 2px;

      z-index: 2000;
    }

    &__i {
      background-color: #0e71f2;
      border-radius: 100%;
      color: white;
      line-height: 18px;
      margin-left: 4px;
      text-align:center;
      width: 18px;

      display: inline-block;
    }
  }

  .tooltip {
    h3 { 
      background-color: #ededed;
      font-size: 1rem; 
      margin: 0;
      padding: $tooltipPadding;
    }

    h4 { 
      font-size: 0.9rem; 
      margin: 0 0 6px 0;
    }

    h5 { 
      margin: 0; 

      &.marine { color: $marineColor } 
      &.terrestrial { color: $terrestrialColor } 
    }

    &__section {
      padding: $tooltipPadding;
    }

    &--marine { background-color: $marineColorBg; }
    &--terrestrial { background-color: $terrestrialColorBg; }
  }

  .total { 
    margin: 2px 0 6px 23px; 
    display: block;
  }
</style>
