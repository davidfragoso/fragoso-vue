<script setup lang="ts">
import { RouterView } from 'vue-router';
</script>

<template>

  <RouterView />

</template>

<style scoped>
header {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  background-color: #f8f8f8;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.logo-wrapper {
  margin-bottom: 1rem;
}

.logo {
  max-width: 100%;
  height: auto;
}

nav {
  display: flex;
  gap: 1rem;
}

nav a {
  text-decoration: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  background-color: #333;
  color: #fff;
  transition: background-color 0.3s, color 0.3s;
}

nav a:hover {
  background-color: #555;
}

@media (min-width: 768px) {
  header {
    flex-direction: row;
    justify-content: space-between;
  }

  nav {
    margin-top: 1rem;
  }
}
</style>
