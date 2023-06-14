<template>
  <header>
    <button @click="showForm = true">Открыть форму</button>
      <AddTask v-if="showForm" @onAddTask="addTask"> </AddTask>
  </header>
  <div class="page">
    <Droppable v-for="category in categories" :key="category.id" :category="category" @drop="onDrop" class="droppable">
      <Draggable v-for="item in items.filter(x => x.categoryId == category.id)" :key="item.id" :item="item"
        class="draggable" />
    </Droppable>
  </div>
</template>

<script>
import Draggable from './components/Draggable.vue';
import Droppable from './components/Droppable.vue';
import AddTask from './components/AddTask.vue';
import { ref, watch } from 'vue';

export default {
  name: 'App',
  components: {
    Draggable,
    Droppable,
    AddTask
  },

  setup() {
    const items = ref([
      {
        id: 1,
        title: 'kanban',
        description: 'Составить таблицу рисков создание проекта “Мир покупок”',
        responsible: 'Менеджер проекта',
        status: 'Очередь',
        categoryId: 1
      },
      {
        id: 2,
        title: 'fact',
        description: 'Утвердить ТЗ с заказчиком по проекту “Мир покупок”',
        responsible: 'Менеджер проекта',
        status: 'Очередь',
        categoryId: 1
      },
      {
        id: 3,
        title: 'mgtu',
        description: 'Согласовать дополнительное соглашение в связи с изменениями функционала интернет-магазина “Тор”',
        responsible: 'Менеджер проекта',
        status: 'Очередь',
        categoryId: 1
      },
      {
        id: 4,
        title: 'kanban',
        description: 'Сделать адаптив страницы company.php проекта “Альян”',
        responsible: 'Frontend-разработчик',
        status: 'Очередь',
        categoryId: 1
      },
      // {
      //   id: 5,
      //   title: 'fact',
      //   description: 'Создать форму обратной связи проекта “Альянс”',
      //   responsible: 'Frontend-разработчик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 6,
      //   title: 'mgtu',
      //   description: 'Создать анимацию для кнопки входа в личный магазин проекта “Top”',
      //   responsible: 'Frontend-разработчик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 7,
      //   title: 'mgtu',
      //   description: 'Создать слайдер на главной странице проекта “Top”',
      //   responsible: 'Frontend-разработчик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 8,
      //   title: 'kanban',
      //   description: 'Реализовать запросы к базе данных, в которых выводится вся информация о клиентах проекта “Альянс”',
      //   responsible: 'Backend-разработчик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 9,
      //   title: 'fact',
      //   description: 'Исправить ошибку ввода данных с формы регистрации проекта “Альянс”. Логины не сохранятся в базе данных',
      //   responsible: 'Backend-разработчик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 10,
      //   title: 'mgtu',
      //   description: 'Создать компонент Битрикса вывода одного товара на экран проекта “Альянс”',
      //   responsible: 'Backend-разработчик',
      //   status: 'Очередь',
      //   categoryId: 1
      // }, {
      //   id: 11,
      //   title: 'kanban',
      //   description: 'Провести анализ данных компаний “Вкусно и запятая”',
      //   responsible: 'Аналитик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 12,
      //   title: 'fact',
      //   description: 'Описание use cases проекта “Вкусно и запятая”',
      //   responsible: 'Аналитик',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 13,
      //   title: 'mgtu',
      //   description: 'Отрисовать дизайн макета главной страницы проекта “Миа”',
      //   responsible: 'Дизайнер',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 14,
      //   title: 'mgtu',
      //   description: 'Отрисовать логотип для проекта “Альянс”',
      //   responsible: 'Дизайнер',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 15,
      //   title: 'fact',
      //   description: 'Отрисовать макет главной страницы проекта “Мир покупок”',
      //   responsible: 'Дизайнер',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 16,
      //   title: 'mgtu',
      //   description: 'Провести пресейл проекта “Вкусно и запятая”',
      //   responsible: 'Директор по продажам',
      //   status: 'Очередь',
      //   categoryId: 1
      // },
      // {
      //   id: 17,
      //   title: 'mgtu',
      //   description: 'Закрыть вакансию “Маркетолог”',
      //   responsible: 'hr-специалист',
      //   status: 'Очередь',
      //   categoryId: 1
      // }
    ])
    const categories = ref([
      {
        id: 1,
        title: 'Очередь',
        count_task: countTask(1),
        bgColor:'#b3d8ff'
      },
      {
        id: 2,
        title: 'Планирование',
        count_task: countTask(2),
        bgColor:'#9fc4ff'
      },
      {
        id: 3,
        title: 'В работе',
        count_task: countTask(3),
        bgColor:'#7ac1ff'
      },
      {
        id: 4,
        title: 'Проверка',
        count_task: countTask(4),
        bgColor:'#ff9b8f'
      },
      {
        id: 5,
        title: 'Готово',
        count_task: countTask(5),
        bgColor:'#c5e1a5'
      },
    ])
    
    let showForm = ref(false)

    const addTask = ({title,description,responsible}) =>{
      items.value = [...items.value, {id: items.value[items.value.length - 1].id + 1, title, description, responsible ,status:'Очередь',  categoryId:1}]
      showForm = false
    }  

    function onDrop(itemId, categoryId) {
      items.value = items.value.map(x => {
        if (x.id === itemId)
          x.categoryId = categoryId
        return x
      })
    }
    function checkStatus(itemId) {
      const item = items.value.find(x => x.id === itemId)
      if (item) {
        const category = categories.value.find(x => x.id === item.categoryId)
        if (category) {
          item.status = category.title
        }
      }
    }
    function countTask(categoryId) {
      return items.value.filter(item => item.categoryId === categoryId).length
    }
    watch(items, () => {
      categories.value.forEach(category => {
        category.count_task = countTask(category.id)
      })
    })
    watch(items, (newItems) => {
      newItems.forEach(item => {
        checkStatus(item.id)
      })
    })
    return {
      items,
      categories,
      onDrop,
      countTask,
      checkStatus,
      addTask,
      showForm
    }
  }
}
</script>

<style>
.page {
  padding: 20px 20px;
  display: grid;
  justify-content: space-around;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  column-gap: 25px;
  row-gap: 25px;
}
</style>