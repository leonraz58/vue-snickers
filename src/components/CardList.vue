<script setup>
import Card from '@/components/Card.vue'

defineProps({
  items: Array
})

const onClickAdd = () => {
  alert(1)
}

const onClickFavourite = () => {
  alert(2)
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :imageUrl="item.imageUrl"
      :title="item.title"
      :price="item.price"
      :is-added="true"
      :is-favorite="true"
      :onClickAdd="onClickAdd"
      :on-click-favorite="onClickFavourite"
    />
  </div>
</template>
