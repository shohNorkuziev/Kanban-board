<template>
  <div @dragstart="onDragStart" draggable="true" class="draggable">
    <h2 class="title">{{ item.title }}</h2>
    <div class="description">{{ item.description }}</div>
    <div class="important">{{ item.responsible }}</div>
    <div class="status">{{ item.status }}</div>
  </div>
</template>

<script>
import { computed } from 'vue'
export default {
  props: {
    item: Object,
    category: Object
  },
  methods: {
    onDragStart(event) {
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
      event.dataTransfer.setData('itemId', this.item.id)
    }
  },
}
</script>

<style scoped>
.draggable:hover {
  cursor: pointer;
  opacity: 0.7;
  transition: all 0.3s;
}

.draggable {
  padding: 9px;
  border-radius: 9px;
  background: #FFFFFF;

  display: grid;
  row-gap: 15px;
  justify-content: center;
  align-items: center;
  height: min-content;

  border-radius: 5px;
  padding: 8px;

}

.title {
  font-family: Inter;
  font-size: 24px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0em;
  text-align: left;

  height: fit-content;
  width: 192px;
  left: 8px;
  top: 8px;
  border-radius: nullpx;

}

.description {
  color: #6C6C6C;
  font-family: Inter;
  font-size: 15px;
  font-weight: 400;
  line-height: 20px;
  letter-spacing: 0em;
  text-align: left;
}

.important {
  font-family: 'Inter';
  font-style: normal;
  font-weight: 400;
  font-size: 15px;
  line-height: 20px;
  color: #6C6C6C;
}

.status {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 5px;
  width: fit-content;
  height: 19px;
  border-radius: 100px;
}
</style>