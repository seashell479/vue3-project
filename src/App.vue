<template>
  <div class="container">
    <h1 class="text-center">🐯To-Do List🐯</h1>
    <form class="d-flex" @submit.prevent="onSubmit">
      <div class="flex-grow-1 me-2">
        <input class="form-control" type="text" v-model="todo" placeholder="새로운 내용 입력" />
      </div>
      <button class="btn btn-primary" type="submit">추가</button>
    </form>
    <div v-if="hasError" class="text-danger">
      내용은 무조건 입력하셔야 합니다!!
    </div>
    <div v-for="todo in todoList" :key="todo.id">
      <div class="card mt-2">
        <div class="card-body p-2">
          <div class="form-check">
            <input class="form-check-input" type="checkbox" v-model="todo.completed">
            <label class="form-check-label" :class="{ completed: todo.completed }">
              {{ todo.content }}
            </label>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const todo = ref("");
    const todoList = ref([]); // 배열 요소
    const hasError = ref(false);
    const completedStyle = {
      textDecoration: "line-through",
      color: "gray",
    }

    function onSubmit() {
      if (todo.value === "") {
        hasError.value = true;
      } else {
        todoList.value.push({
          id: Date.now(),
          content: todo.value,
          completed: false, //체크박스 연동
        });
        hasError.value = false;
        todo.value = "";
      }
    }

    return { todo, todoList, onSubmit, hasError, completedStyle }
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
