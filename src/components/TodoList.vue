<template>
  <div v-for="(todo, index) in todoList" :key="todo.id">
    <div class="card mt-2">
      <div
        class="card-body p-2 d-flex align-items-center"
        style="cursor: pointer"
        @click="moveToPage(todo.id)"
      >
        <div class="form-check flex-grow-1">
          <input
            class="form-check-input"
            type="checkbox"
            :checked="todo.completed"
            @change="toggleTodo(index, $event)"
            @click.stop
          />
          <label
            class="form-check-label"
            :class="{ completed: todo.completed }"
          >
            <!-- class 바인딩 v-bind 속성을 :class로 지정 -->
            {{ todo.content }}
          </label>
        </div>
        <div>
          <button class="btn btn-danger" @click.stop="onDelete(index)">
            삭제
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useRouter } from "vue-router";

export default {
  props: {
    todoList: {
      type: Array,
      required: true,
    },
  },
  emits: ["toggle-todo", "todo-delete"],
  setup(props, { emit }) {
    const router = useRouter();

    function toggleTodo(index, event) {
      emit("toggle-todo", index, event.target.checked);
    }

    function onDelete(index) {
      emit("todo-delete", index);
    }

    function moveToPage(todoId) {
      console.log(todoId);
      // router.push("/todolist/" + todoId);
      router.push({
        name: "Modify",
        params: {
          id: todoId,
        },
      });
    }

    return { toggleTodo, onDelete, moveToPage };
  },
};
</script>

<style></style>
