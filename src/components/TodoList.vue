<template>
  <h1>Todo List</h1>
  <ul class="list">
    <li><r-input @addTodo="addTodo"></r-input></li>
    <li v-for="(todo, index) in todos" :key="index">
      <todo :index="index" :title="todo.title" @editTodo="editTodo($event)" @deleteTodo="deleteTodo" />
    </li>
  </ul>
</template>

<script>
import Todo from './Todo.vue';
import RInput from './Input.vue';
import { ref } from 'vue';

export default {
  name: 'TodoList',
  components: {
    Todo,
    RInput
  },
  setup() {
    const todos = ref([{ title: 'One' }, { title: 'todo' }, { title: 'at' }, { title: 'the' }, { title: 'time' }]);

    function addTodo(newTitle) {
      var obj = { title: '' };
      var prop = 'title';
      obj[prop] = newTitle;
      todos.value.push(obj);
    }

    function editTodo(data) {
      var obj = { title: '' };
      var prop = 'title';
      obj[prop] = data.title;
      todos.value[data.index] = obj;
    }

    function deleteTodo(index) {
      todos.value.splice(index, 1);
    }

    return {
      todos,
      addTodo,
      editTodo,
      deleteTodo
    };
  }
};
</script>

<style>
.list {
  list-style: none;
}

.list > li {
  background: beige;
  padding: 10px;
  max-width: 80%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 10px;
}
</style>
