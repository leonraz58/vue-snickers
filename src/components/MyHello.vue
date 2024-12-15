<script setup>
import { ref } from 'vue'

let count = ref(0)

function increment() {
  count.value++
}

// function updateCount(event) {
//   count.value = Number(event.target.value)
// }
</script>

<template>
  <h1>{{ count }}</h1>
  <button @click="increment">+</button>
<!--  <input @input="updateCount" />-->
  <input v-model="count" />
  <input @keyup.enter="increment" />
</template>

<!--<script>-->
<!--export default {-->
<!--  data() {-->
<!--    return {-->
<!--      count: 0,-->
<!--    }-->
<!--  },-->
<!--  methods: {-->
<!--    increment() {-->
<!--      this.count++-->
<!--    }-->
<!--  }-->
<!--}-->
<!--</script>-->

<!--<template>-->
<!--  <h1>{{ count }}</h1>-->
<!--  <button @click="increment">+</button>-->
<!--</template>-->
