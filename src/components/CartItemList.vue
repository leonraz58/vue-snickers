<script setup lang="ts">
import CartItem from '@/components/CartItem.vue'
import { inject } from 'vue'

const { cart } = inject('cart')
</script>

<template>
  <div class="flex flex-col flex-1 justify-between">
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :image-url="item.imageUrl"
    />
  </div>
</template>
