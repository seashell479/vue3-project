<template>
  <h1>Modify Page 😋</h1>
  <div class="mb-2">
    <label>상태</label>
    <div>
      <button
        class="btn"
        :class="beforeTodo.completed ? 'btn-success' : 'btn-danger'"
        @click="toggleTodoStatus"
      >
        {{ beforeTodo.completed ? "Completed" : "Incomplete" }}
      </button>
    </div>
  </div>
  <form @submit.prevent="onUpdate">
    <div class="form-group">
      <label>내용</label>
      <textarea
        v-model="beforeTodo.content"
        class="form-control"
        rows="3"
      ></textarea>
    </div>
    <div class="mt-2">
      <button class="btn btn-primary">저장</button>
      <button class="btn btn-outline-dark ms-2" @click="moveTotodoListPage">
        취소
      </button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
import { useRoute, useRouter } from "vue-router";
import { ref } from "vue";

export default {
  setup() {
    const route = useRoute();
    const router = useRouter();
    const beforeTodo = ref({});

    async function getTodo() {
      const res = await axios.get(
        "http://localhost:3000/todolist/" + route.params.id
      );
      beforeTodo.value = res.data;
    }

    function toggleTodoStatus() {
      beforeTodo.value.completed = !beforeTodo.value.completed;
    }

    getTodo();

    function moveTotodoListPage() {
      router.push({
        name: "TodoList",
      });
    }

    async function onUpdate() {
      const res = await axios.patch(
        "http://localhost:3000/todolist/" + route.params.id,
        {
          content: beforeTodo.value.content,
          completed: beforeTodo.value.completed,
        }
      );
      router.push({
        name: "TodoList",
      });
    }

    return { beforeTodo, toggleTodoStatus, moveTotodoListPage, onUpdate };
  },
};
</script>

<style></style>
