<template>
  <div id="app">
    <grid :items="items" :size="15" />
  </div>
</template>

<script>
import Grid from './components/Grid.vue'
import {getGridItem} from './svc/grid'

export default {
  name: 'app',
  data () {
    return {
      items: [],
    }
  },
  created () {
    getGridItem()
      .then(x => this.items = x)
      .catch(e => console.log('error', e))
  },
  components: {
    Grid,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
