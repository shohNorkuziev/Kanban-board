<script>
// import Draggable from './Draggable.vue';
import { ref } from 'vue';

export default {
  name: 'App',
  // components: {
  //   Draggable,
  // },
  setup() {
    const items = ref([
      {
        id:1,
        title:'kanban',
        description:'take the kanban board',
        important:'important',
        status:'new',
        categoryId:1
      },
      {
        id:2,
        title:'fact',
        description:'take the kanban fact',
        important:'important',
        status:'new',
        categoryId:1
      },
      {
        id:3,
        title:'mgtu',
        description:'take the kanban mgtu',
        important:'important',
        status:'new',
        categoryId:1
      }
    ])
    const categories = ref([
      {
        id:1,
        title:'to do',
        count_task:10
      },
      {
        id:2,
        title:'in progress',
        count_task:5
      }
    ])

    function onDragStart(event, item) {
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
      event.dataTransfer.setData('itemId', item.id)
    }
    function onDrop(event, categoryId) {
      const itemId = parseInt(event.dataTransfer.getData('itemId'))
      items.value = items.value.map(x=>{
        if(x.id === itemId)
        x.categoryId = categoryId
        return x
      })
    }
    

    return {
      items,
      categories,
      onDragStart,
      onDrop
    }
  }
}
</script>

<template>
<div class="page">
  <div 
  v-for="category in categories" 
  v-bind:key="category.id" 
  @drop="onDrop($event,category.id)" 
  class="droppable"
  @dragover.prevent
  @dragenter.prevent
  >
    <div class="title">{{ category.title }}</div>
    <div class="count_task">{{ category.count_task }}</div>
    <div 
      v-for="item in items.filter(x => x.categoryId == category.id)" 
      v-bind:key="item.id" 
      @dragstart="onDragStart($event,item)" 
      draggable="true"
      class="draggable">
      <div class="title">{{ item.title }}</div>
      <div class="description">{{ item.description }}</div>
      <div class="important">{{ item.important }}</div>
      <div class="status">{{ item.status }}</div>
    </div>
  </div>
</div>
</template>

<style>
.page{
  display: grid;
  justify-content: space-around;
  grid-template-columns: 1fr 1fr;
}
.droppable {
  width: 250px;
  display: grid;
  background-color: #101204;
  color: #B6C2CF;
  padding: 15px 15px;
  gap: 10px;
  grid-template-columns: 150px;
  grid-template-rows: 20px 20px 1fr;
  border-radius: 12px;
}

.draggable {
  padding: 9px;
  border-radius: 9px;
  background-color: #22272B;
  color: #B6C2CF;
  display: grid;
  gap: 5px;
  width: 150px;
  height: 130px;
  justify-content: center;
  align-items: center;
}
</style>