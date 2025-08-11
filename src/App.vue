<script setup>
import { RouterLink, RouterView } from 'vue-router';
</script>

<template>
  <header>
    <div class="p-4">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/week-1">Week 1</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped></style>
