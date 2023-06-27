<template>
  <h1>Modify Page 😋</h1>
  <form>
    <div class="form-group">
      <label>내용</label>
      <textarea class="form-control" rows="3"></textarea>
    </div>
    <button class="btn btn-primary mt-2">저장</button>
  </form>
</template>

<script>
import axios from "axios";
import { useRoute } from "vue-router";

export default {
  setup() {
    const route = useRoute();

    async function getTodo() {
      const res = await axios.get(
        "http://localhost:3000/todolist/" + route.params.id
      );
      console.log(res.data);
    }
    getTodo();
  },
};
</script>

<style></style>
