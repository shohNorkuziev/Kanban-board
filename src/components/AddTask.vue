<template>
    <form  class="addFrom">
      <div>
        <label for="title">Введите название задачи:</label>
        <input v-model="title" placeholder="Название" type="text" id="title">
      </div>
  
      <div>
        <label for="description">Введите описание задачи:</label>
        <textarea v-model="description" cols="30" rows="10" placeholder="Описание" type="text" id="description"></textarea>
      </div>
  
      <div>
        <label for="responsible">Выберите ответственного:</label>
        <select v-model="responsible" name="" id="responsible">
          <option value="Менеджер проекта">Менеджер проекта</option>
          <option value="Frontend-разработчик">Frontend-разработчик</option>
          <option value="Backend-разработчик">Backend-разработчик</option>
          <option value="Аналитик">Аналитик</option>
          <option value="Дизайнер">Дизайнер</option>
          <option value="Директор по продажам">Директор по продажам</option>
          <option value="hr-специалист">hr-специалист</option>
        </select>
      </div>
  
      <button type="reset" @click="onAddTask">Добавить задачу</button>
    </form>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    props: {
    showForm: {
      type: Boolean,
      required: false
    }
  },
    emits: ['onAddTask'],
    setup(props, { emit }) {
      const title = ref('')
      const description = ref('')
      const responsible = ref('')
  
      const onAddTask = () => {
        if (title.value === '' || description.value === ''|| responsible.value === '') {
          alert('Введите информацию, пожалуйста')
          return false
        }
        emit('onAddTask', { title: title.value, description: description.value, responsible: responsible.value})
        return true
      }

      return {
        title,
        description,
        responsible,
        onAddTask
      }
    },
  }
  </script>

<style scoped>
    .addFrom{
        background-color: #b3d8ff;
        color: #000;
        padding: 20px;
        border-radius: 10px;
        margin: 20px;
    }
    .addFrom label{
        font-weight: bold;
        margin-bottom: 10px;
        display: block;
    }
    .addFrom input, .addFrom textarea, .addFrom select{
        padding: 10px;
        border-radius: 5px;
        border: none;
        margin-bottom: 20px;
        width: 98%;
    }
    .addFrom button{
        background-color: #9fc4ff;
        color: #000;
        padding: 10px 20px;
        border-radius: 5px;
        border: none;
        cursor: pointer;
    }
</style>