<template>
  <div class="justify-content-center text-center mt-3">
    <h1 class="text-primary fw-bold">환영합니다!!😊</h1>
    <hr />
    <figure>
      <blockquote class="blockquote">
        <p class="h6 fw-bold">
          내일의 일을 미리 걱정하지 말라. 내일 당신에게 어떤 일이 일어날지
          아무도 모른다.
          <br />
          내일은 돌아오지만 당신은 영원히 살 수 없으니 당신이 속하지 않는 세상을
          위해 걱정하지 말라.
        </p>
      </blockquote>
      <figcaption class="blockquote-footer">
        <cite title="Source Title" class="h6 fw-bold">Talmud</cite>
      </figcaption>
    </figure>
    <img src="@/assets/main.gif" />
    <hr />
    <div class="d-flex justify-content-center">
      <p class="h5 fw-bold mt-2">✔일정 작성</p>
      <router-link to="/todolist" class="btn btn-success ms-2 fw-bold"
        >GO !</router-link
      >
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
