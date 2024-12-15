<script setup>
import MyHello from '@/components/MyHello.vue'
</script>

<template>
  <MyHello title="Кроссовки Puma" :price="9500" :isAdded="true">
    <button>Добавить</button>
  </MyHello>
  <MyHello isAdded />
  <MyHello>
    <MyHello>
      <button>123</button>
    </MyHello>
  </MyHello>
</template>

<style scoped>
</style>
