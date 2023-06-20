<template>
  <div v-for="(todo, index) in todoList" :key="todo.id">
    <div class="card mt-2">
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input class="form-check-input" type="checkbox" :checked="todo.completed" @change="toggleTodo(index)">
          <label class="form-check-label" :class="{ completed: todo.completed }">
            <!-- class 바인딩 v-bind 속성을 :class로 지정 -->
            {{ todo.content }}
          </label>
        </div>
        <div>
          <button class="btn btn-danger" @click="onDelete(index)">삭제</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todoList: {
      type: Array,
      required: true,
    }
  },
  emits: ["toggle-todo", "todo-delete"],
  setup(props, { emit }) {
    function toggleTodo(index) {
      emit("toggle-todo", index)
    }

    function onDelete(index) {
      emit("todo-delete", index)
    }

    return { toggleTodo, onDelete }
  }
}
</script>

<style></style>