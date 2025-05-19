<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template class="main">
  <div class="outer">
    <RouterView/>
  </div>
</template>

<style>
.outer {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}
</style>
