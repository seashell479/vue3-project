<template>
  <form class="d-flex" @submit.prevent="onSubmit">
    <div class="flex-grow-1 me-2">
      <input class="form-control" type="text" v-model="todo" placeholder="새로운 내용 입력" />
    </div>
    <button class="btn btn-primary" type="submit">추가</button>
  </form>
  <div v-if="hasError" class="text-danger">
    내용은 무조건 입력하셔야 합니다!!
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ["add-todo"],
  setup(props, { emit }) {
    const todo = ref("");
    const hasError = ref(false);

    function onSubmit() {
      if (todo.value === "") {
        hasError.value = true;
      } else {
        emit('add-todo', {
          id: Date.now(),
          content: todo.value,
          completed: false, //체크박스 연동
        });
        hasError.value = false;
        todo.value = "";
      }
    }

    return { todo, hasError, onSubmit }
  }
}
</script>

<style></style>