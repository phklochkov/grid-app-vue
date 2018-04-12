<template>
  <div class="grid-row">
    <grid-item
      v-for="x in size" :key="x"
      :item="grid[size * rowNum + x] || {}"
      :id="size * rowNum + x"
      :itemSize="100 / size" />
  </div>
</template>

<script>
import GridItem from './GridItem.vue'

export default {
  name: 'GridRow',
  props: {
    rowNum: Number,
    size: Number,
    grid: Object,
  },
  components: {
    GridItem,
  }
}
</script>

<style scoped>
  .grid-row {
    display: flex;
    flex-direction: row;
    padding: 5px 0;
  }
</style>

