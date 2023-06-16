<template>
  <div class="container">
    <h1 class="text-center">🐯To-Do List🐯</h1>
    <input class="form-control" type="text" v-model="searchText" placeholder="검색">
    <hr />
    <SimpleForm @add-todo="addTodo" />
    <div v-if="!filteredTodoList.length">
      <!-- 전에 했던 거 v-if="!todoList.length"/v-if="todoList.length == 0" 가능함, v-show도 가능함 -->
      추가된 내용이 없습니다.
    </div>
    <TodoList :todoList="filteredTodoList" @toggle-todo="toggleTodo" @todo-delete="onDelete" />
  </div>
</template>

<script>
import { ref, computed } from "vue";
import SimpleForm from './components/SimpleForm.vue';
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    SimpleForm,
    TodoList,
  },

  setup() {
    const todoList = ref([]); // 배열 요소

    function addTodo(todos) {
      console.log(todos);
      todoList.value.push(todos);
    }

    function toggleTodo(index) {
      console.log(todoList.value[index].completed);
      todoList.value[index].completed = !todoList.value[index].completed;
      console.log(todoList.value[index].completed);
    }

    function onDelete(index) {
      todoList.value.splice(index, 1);
    }

    const searchText = ref("");
    const filteredTodoList = computed(() => {
      if (searchText.value) {
        return todoList.value.filter((loop) => {
          return loop.content.includes(searchText.value);
        })
      }
      return todoList.value;
    })

    return { todoList, addTodo, onDelete, toggleTodo, searchText, filteredTodoList };
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
