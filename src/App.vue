<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <router-link class="navbar-brand" :to="{ name: 'Home' }"
        >Home</router-link
      >
      <ul class="navbar-nav me-auto mb-lg-0">
        <li class="nav-item">
          <router-link
            class="nav-link active"
            aria-current="page"
            :to="{ name: 'TodoList' }"
            >TodoList</router-link
          >
        </li>
      </ul>
    </div>
  </nav>
  <div class="container">
    <router-view />
  </div>
</template>

<script></script>

<style></style>
