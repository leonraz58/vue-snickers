<script setup>
import MyHello from '@/components/MyHello.vue'
</script>

<template>
  <div class="mb-20 bg-amber-100">
  <MyHello title="Кроссовки Puma" :price="9500" :isAdded="true">
    <button>Добавить</button>
  </MyHello>
  </div>
</template>

<style scoped>
</style>
