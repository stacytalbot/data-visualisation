<template>
  <div class="infographic">
    <h2>{{ title }}</h2>
    
    <div class="datasets">
      <dataset v-for="dataset, index in datasets"
        :key="index"
        :title="dataset.title"
        :year="dataset.year"
        :categories="dataset.categories"
        :options="options">
      </dataset>
    </div>
  </div>
</template>

<script>
  import Dataset from './Dataset'

  export default {
    name: 'infographic',

    components: { Dataset },

    props: {
      json: { required: true }
    },

    data () {
      return {
        title: '',
        datasets: [],
        options: []
      }
    },

    created: function () {
      this.title = this.json.title
      this.datasets = this.json.data
      this.options = this.json.options
    }
  }
</script>

<style lang="scss">
  .infographic {
    padding: 20px;
  }
  
  h2 {
    margin-bottom: 24px;
  }
  
  .datasets {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
  }
</style>
