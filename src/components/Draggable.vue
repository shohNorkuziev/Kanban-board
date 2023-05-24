<template>
    <div 
      @dragstart="onDragStart"
      draggable="true"
      class="draggable"
      >
      <div class="title">{{ item.title }}</div>
      <div class="description">{{ item.description }}</div>
      <div class="important">{{ item.responsible }}</div>
      <div class="status">{{ item.status }}</div>
    </div>
  </template>
  
  <script>
  
  export default {
    props: {
      item: Object,
    },
    methods: {
      onDragStart(event) {
        event.dataTransfer.dropEffect = 'move'
        event.dataTransfer.effectAllowed = 'move'
        event.dataTransfer.setData('itemId', this.item.id)
      }
    }
  }
  </script>
  
  <style>
  .draggable {
    padding: 9px;
    border-radius: 9px;
    background-color: #22272B;
    color: #B6C2CF;
    display: grid;
    gap: 5px;
    width: 90%;
    justify-content: center;
    align-items: center;
    height: min-content; 

  }
  </style>