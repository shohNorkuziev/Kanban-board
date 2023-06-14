<template>
  <div 
    @drop="onDrop" 
    class="droppable"
    @dragover.prevent
    @dragenter.prevent
    :style="{backgroundColor:category.bgColor}"
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
  display: flex;
  padding: 24px 24px;
  gap: 10px;
  border-radius: 12px;
  align-items: start;
  flex-direction: column;
  border: 1px solid #D6D8DB;
}
.title{
  font-family: Inter;
font-size: 24px;
font-weight: 700;
line-height: 28px;
letter-spacing: 0px;
text-align: left;

}
</style>