<template>
  <div :class="['grid-item', item.title ? 'draggable' : '',]" :style="style"
    :draggable="!!item.title" @dragover.prevent @dragstart.stop="onDragStart"
    @dragenter="onDragEnter" @dragleave="onDragLeave" @drop.stop="onDrop">
    <div class="grid-item-title">{{ item.title }}</div>
  </div>
</template>

<script>
export default {
  name: 'GridItem',
  props: {
    id: Number,
    item: Object,
    itemSize: Number,
  },
  methods: {
    clearStyle (elm) {
      elm && elm.classList.remove('over')
    },
    onDragStart (e) {
      e.dataTransfer.setData('text/grid', this.id)
    },
    onDragEnter (e) {
      e.currentTarget.classList.add('over')
    },
    onDragLeave (e) {
      this.clearStyle(e.currentTarget)
    },
    onDrop (e) {
      const id = +e.dataTransfer.getData('text/grid')
      this.$eventHub.$emit('grid-drop', id, this.id)
      this.clearStyle(e.currentTarget)
    }
  },
  computed: {
    style () {
      return {
        margin: '0 5px',
        width: `${this.itemSize}vw`,
        height: `calc(${this.itemSize}vw - 10px)`, // 10px - value of margin.
        backgroundColor: this.item.color,
      }
    }
  }
}
</script>

<style scoped>
  .grid-item {
    background-color: transparent;
    border-radius: 4px;
    box-shadow: 0px 0px 0px 2px #a9a9a9;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .grid-item > .grid-item-title {
    pointer-events: none;
  }

  .grid-item.draggable {
    cursor: -webkit-grab;
    cursor: grab;
  }

  .grid-item.over {
    background-color: #28abe3;
    box-shadow: 0px 0px 5px 3px #28abe3;
  }
</style>

