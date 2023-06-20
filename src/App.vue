<template>
  <div class="container">
    <h1 class="text-center">🐯To-Do List🐯</h1>
    <input class="form-control" type="text" v-model="searchText" placeholder="검색">
    <hr />
    <SimpleForm @add-todo="addTodo" />
    <div class="text-danger" v-if="axiosErrorMessage.length != 0"> <!-- 문자열 값이 있을 때 -->
      {{ axiosErrorMessage }} <!-- true일 때 에러메세지 출력됨 -->
    </div>
    <div v-if="!filteredTodoList.length">
      <!-- 전에 했던 거 v-if="!todoList.length"/v-if="todoList.length == 0" 가능함, v-show도 가능함 -->
      추가된 내용이 없습니다.
    </div>
    <TodoList :todoList="filteredTodoList" @toggle-todo="toggleTodo" @todo-delete="onDelete" />
    <hr />
    <nav aria-label="Page navigation example">
      <ul class="pagination">
        <li class="page-item">
          <a class="page-link" href="#">이전</a>
        </li>
        <li v-for="loop in numberOfpages" :key="loop" class="page-item" :class="currentPage === loop ? 'active' : ''">
          <a class="page-link" href="#">{{ loop }}</a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">다음</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import SimpleForm from './components/SimpleForm.vue';
import TodoList from "./components/TodoList.vue";
import axios from "axios";

export default {
  components: {
    SimpleForm,
    TodoList,
  },

  setup() {
    const todoList = ref([]); // 배열 요소
    const axiosErrorMessage = ref([]);
    const numberOfTodoList = ref(0); // 전체 글 개수
    const currentPage = ref(1); // 변경할 page 번호
    const limit = 5; // 페이지에서 나올 글의 제한 개수, 어떤 상황이든 5개로 표현될거기 때문에 ref로 선언할 필요 x

    const numberOfpages = computed(() => {
      return Math.ceil(numberOfTodoList.value / limit);
    })

    async function getTodoList() {
      axiosErrorMessage.value = "";
      try {
        const res = await axios.get(
          `http://localhost:3000/todoList?_page=${currentPage.value}&_limit=${limit}`
        );
        numberOfTodoList.value = res.headers['x-total-count'];
        todoList.value = res.data;
      } catch (err) {
        console.log(err);
        axiosErrorMessage.value = "네트워크 에러가 발생했어요. 😥";
      }
    }

    getTodoList();

    async function addTodo(todos) { // 동기식
      axiosErrorMessage.value = ""; // 에러 초기화
      try {
        const res = await axios.post("http://localhost:3000/todoList", {
          content: todos.content,
          completed: todos.completed,
        });
        todoList.value.push(res.data);
      } catch (err) { // 에러 났을 때
        axiosErrorMessage.value = "네트워크 에러가 발생했어요. 😥";
        console.log(err);
      }
    }

    // function addTodo(todos) { // 비동기식 
    //   axiosErrorMessage.value = ""; // 에러 초기화
    //   axios
    //     .post("http://localhost:3000/todoList", {
    //       content: todos.content,
    //       completed: todos.completed,
    //     })
    //     .then((res) => { // 정상일 때
    //       console.log(res);
    //       todoList.value.push(todos);
    //       console.log(todoList);
    //     })
    //     .catch((err) => { // 에러 났을 때
    //       axiosErrorMessage.value = "네트워크 에러가 발생했어요. 😥";
    //       console.log(err);
    //     });
    // }

    async function toggleTodo(index) {
      axiosErrorMessage.value = "";
      const id = todoList.value[index].id;
      try {
        await axios.patch("http://localhost:3000/todoList/" + id, {
          completed: !todoList.value[index].completed, // db.json에서 false를 true로 바꿔주는 것
        })
      } catch (err) {
        axiosErrorMessage.value = "네트워크 에러가 발생했어요. 😥";
        console.log(err);
      }
      todoList.value[index].completed = !todoList.value[index].completed; // 배열에서 false를 true로 바꿈
      // console.log(todoList.value[index].completed);
      // todoList.value[index].completed = !todoList.value[index].completed;
      // console.log(todoList.value[index].completed);
    }

    async function onDelete(index) {
      axiosErrorMessage.value = ""; // 에러 초기화
      const id = todoList.value[index].id;
      try {
        const res = await axios.delete("http://localhost:3000/todoList/" + id);
        console.log(res);
        todoList.value.splice(index, 1);
      } catch (err) { // 에러 났을 때
        axiosErrorMessage.value = "네트워크 에러가 발생했어요. 😥";
        console.log(err);
      }
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

    return {
      todoList,
      addTodo,
      onDelete,
      toggleTodo,
      searchText,
      filteredTodoList,
      axiosErrorMessage,
      numberOfpages,
      currentPage,
    };
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
