<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import CardList from '@/components/CardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get('https://f0a3cdde629e5968.mokky.dev/favorites?_relations=items')
    console.log(data)
    favorites.value = data.map(obj => obj.item)

    console.log(favorites)
  } catch (err) {
    console.log(err)
  }
})
</script>
<template>
  <h1>Мои закладки</h1>

  <CardList :items="favorites"/>
</template>
