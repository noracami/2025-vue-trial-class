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

<style scoped>
@reference './assets/main.css';

nav {
  @apply flex gap-8;
}

nav a {
  @apply underline p-8 transition duration-300;
}

nav a:hover {
  @apply bg-gray-200 dark:bg-gray-700 scale-125 no-underline;
}
</style>
