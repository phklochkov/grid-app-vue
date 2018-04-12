<template>
  <div class="grid">
    <grid-row
      v-for="(r, i) in size"
      :key="r"
      :rowNum="i"
      :size="size"
      :grid="grid" />
  </div>
</template>

<script>
import GridRow from './GridRow.vue'

export default {
  name: 'Grid',
  data () {
    return { grid: {}, }
  },
  props: {
    size: Number,
    items: Array,
  },
  created () {
    this.$eventHub.$on('grid-drop', this.onDrop)
  },
  beforeDestroy() {
    this.$eventHub.$off('grid-drop')
  },
  methods: {
    makeList (length) {
      return [...Array(Math.pow(length, 2)).keys()]
    },
    generateGrid () {
      const grid = {}

      this.items.forEach(x => grid[x.id] = x)
      this.makeList(this.size).forEach(x => {
        const v = grid[x+1]
        grid[x+1] = v ? v : {id: x+1}
      })

      this.grid = grid
    },
    onDrop (id, target) {
      if (id && target) {
        this.grid = {...this.grid, [target]: this.grid[id], [id]: this.grid[target]}
      }
    },
  },
  watch: {
    items () {
      this.generateGrid()
    }
  },
  components: {
    GridRow,
  }
}
</script>
