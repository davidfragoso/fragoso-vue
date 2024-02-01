<script setup lang="ts">
import { RouterView } from 'vue-router';
</script>

<template>
  <header>
    <div class="logo-wrapper">
        <RouterView />
    </div>
  </header>

</template>

<style scoped>
header {
  background-color: rgba(125, 150, 144, 0.55);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  box-shadow: 0 20px 100px rgba(40, 39, 39, 0.968);
}

.logo-wrapper {
  text-align: center;
  padding: 0 1rem 0 1rem;

}
</style>