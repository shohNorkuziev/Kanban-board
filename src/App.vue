<template>
  <div class="page">
    <Droppable 
      v-for="category in categories" 
      :key="category.id" 
      :category="category" 
      @drop="onDrop"
      class="droppable"
    >
      <Draggable 
        v-for="item in items.filter(x => x.categoryId == category.id)" 
        :key="item.id" 
        :item="item"
        class="draggable"
      />
    </Droppable>
  </div>
</template>

<script>
import Draggable from './components/Draggable.vue';
import Droppable from './components/Droppable.vue';
import { ref } from 'vue';

export default {
  name: 'App',
  components: {
    Draggable,
    Droppable
  },
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
        title:'Очередь',
        count_task:10
      },
      {
        id:2,
        title:'Планирование',
        count_task:5
      },
      {
        id:3,
        title:'В работе',
        count_task:5
      },
      {
        id:4,
        title:'Проверка',
        count_task:5
      },
      {
        id:5,
        title:'Готово',
        count_task:5
      },
    ])

    function onDrop(itemId, categoryId) {
      items.value = items.value.map(x=>{
        if(x.id === itemId)
        x.categoryId = categoryId
        return x
      })
    }
    

    return {
      items,
      categories,
      onDrop
    }
  }
}
</script>

<style>
.page{
  padding: 20px 20px;
  display: grid;
  justify-content: space-around;
  grid-template-columns:repeat(5, 1fr);
  column-gap: 25px;
}
</style>