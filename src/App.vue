<script setup lang="ts">

import Card from 'primevue/card'
import { ref } from 'vue';

let show = ref(false);

let cards = [
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  },
  {
    title: 'Card',
    description: 'Card description'
  }
]
</script>

<template>
  <div class="cards-container">
    <div v-for="card in cards" class="card-container">
      <Transition name="flip">
        <Card @click="show = !show" class="card">
          <template #title>{{ card.title }}</template>
          <template v-if="show" #content>{{ card.description }}</template>
        </Card>
      </Transition>
    </div>
  </div>
</template>

<style scoped>
.cards-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}
.card {
  color: white;
  background-color: rgb(45, 45, 174);
  border-radius: 5px;
}
</style>
