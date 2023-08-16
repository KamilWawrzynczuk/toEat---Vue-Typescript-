<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="wrapper">
    <h1>ToEAT</h1>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/dishes">Dishes</RouterLink>
  </div>
  <RouterView />
</template>

<style scoped></style>
