<script setup>
import Card from '@/components/Card.vue'

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
      imageUrl="/sneakers/sneakers-1.jpg"
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      :price="1205"
      :is-added="true"
      :is-favorite="true"
      :onClickAdd="onClickAdd"
      :on-click-favorite="onClickFavourite"
    />
  </div>
</template>
