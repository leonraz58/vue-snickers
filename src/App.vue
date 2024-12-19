<script setup>
import Header from '@/components/Header.vue'
import CardList from '@/components/CardList.vue'
import Drawer from '@/components/Drawer.vue'
import { onMounted, provide, reactive, ref, watch } from 'vue'
import axios from 'axios'

const items = ref([])

const drawerOpen = ref(false)

const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

provide('cartActions', {
  closeDrawer,
  openDrawer,
})

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const fetchFavourites = async () => {
  try {

    const { data: favorites } = await axios.get('https://f0a3cdde629e5968.mokky.dev/favorites')
    items.value = items.value.map(item => {
      const favorite = favorites.find(favorite => favorite.itemId === item.id)

      if (!favorite) {
        return item
      }
      console.log(favorite)
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })

    console.log(items.value)
  } catch (e) {
    console.log(e)
  }
}

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        itemId: item.id
      }

      item.isFavorite = true

      const { data } = await axios.post('https://f0a3cdde629e5968.mokky.dev/favorites', obj)

      item.favoriteId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`https://f0a3cdde629e5968.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }

  } catch (err) {
    console.log(err)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get('https://604781a0efa572c1.mokky.dev/items', {params})
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }))
  } catch (e) {
    console.log(e)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavourites()
})

watch(filters, fetchItems)

</script>

<template>
    <Drawer v-if="drawerOpen"/>

  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14">
    <Header @open-driver="openDrawer" />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="поиск" />
            <input
              @input="onChangeSearchInput"
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus: border-gray-400"
              placeholder="Поиск..."
            />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" @add-to-favorite="addToFavorite" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
