<script setup>
import { ref, computed } from 'vue'
const name = 'counter'
const counter = ref(0)

const arrayFavorites = ref([])

const increment = () => {
  counter.value++
}
const decrement = () => {
  counter.value--
}
const reset = () => {
  counter.value = 0
}

const blockBtn = computed(() => {
  const numSearch = arrayFavorites.value.find(num => num === counter.value)
  if (numSearch === 0) return true
  return numSearch ? true : false
})

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})

const add = () => {
  arrayFavorites.value.push(counter.value)
}
</script>

<template>
  <div class="container text-center mt-3">
    <h1>{{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">increment</button>
      <button @click="decrement" class="btn btn-danger">decrement</button>
      <button @click="reset" class="btn btn-secondary">reset</button>
      <button @click="add" :disabled="blockBtn" class="btn btn-primary">Add</button>
    </div>
    <ul class="list-group mt-4">
      <h2>Favorite numbers list</h2>
      <li class="list-group-item" v-for="(num, index) in arrayFavorites" :key="index">{{ num }}</li>
    </ul>
  </div>
</template>

<style scoped>
h1 {
  color: rgb(42, 41, 41);
  font-weight: 900;
}

.negative {
  color: red;
}

.positive {
  color: blue;
}

.zero {
  color: black;
}
</style>
