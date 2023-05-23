<template>
  <div 
    @drop="onDrop" 
    class="droppable"
    @dragover.prevent
    @dragenter.prevent
    >
    <div class="title">{{ category.title }}</div>
    <div class="count_task">{{ category.count_task }}</div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    category: Object
  },
  methods: {
    onDrop(event) {
      const itemId = parseInt(event.dataTransfer.getData('itemId'))
      this.$emit('drop', itemId, this.category.id)
    }
  }
}
</script>

<style>
.droppable {
  display: grid;
  background-color: #101204;
  color: #B6C2CF;
  padding: 15px 15px;
  gap: 10px;
  grid-template-columns: 150px;
  grid-template-rows: 20px 20px 1fr;
  border-radius: 12px;
}
</style>