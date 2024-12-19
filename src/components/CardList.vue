<script setup>
import Card from '@/components/Card.vue'
import { inject } from 'vue'

defineProps({
  items: Array
})

const onClickAdd = () => {
  alert(1)
}

const addToFavorite = inject('addToFavorite')

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :imageUrl="item.imageUrl"
      :title="item.title"
      :price="item.price"
      :is-added="true"
      :is-favorite="item.isFavorite"
      :onClickAdd="onClickAdd"
      :on-click-favorite="() => addToFavorite(item)"
    />
  </div>
</template>
