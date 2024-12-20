<script setup>
import Card from '@/components/Card.vue'

defineProps({
  items: Array,
  isFavorites: Boolean
})

const emit = defineEmits(['addToFavorite', 'addToCart'])

//const addToFavorite = inject('addToFavorite')

</script>

<template>
  <div class="grid grid-cols-4 gap-5" v-auto-animate>
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :imageUrl="item.imageUrl"
      :title="item.title"
      :price="item.price"
      :is-added="item.isAdded"
      :is-favorite="item.isFavorite"
      :on-click-favorite="isFavorites ? null : () => emit('addToFavorite', item)"
      :on-click-add="isFavorites ? null : () => emit('addToCart', item)"
    />
  </div>
</template>
