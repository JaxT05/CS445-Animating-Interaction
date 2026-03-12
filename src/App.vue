<script setup lang="ts">
import Card from 'primevue/card'
import { ref } from 'vue';

let cards = ref([
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false,
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  },
  {
    title: 'Card',
    description: 'Card description',
    isActive: false
  }
]);

const handleCardClick = (card) => {
  card.isActive = !card.isActive;
  console.log(card.isActive);
}
</script>

<template>
  <div class="cards-display">
    <div v-for="card in cards" class="card-container" :key="card.title">
      <div @click="handleCardClick(card)">
        <Transition name="card-flip" mode="out-in">
        <Card v-if="card.isActive" key="front" :class="{ active: card.isActive }" class="card">
            <template class="card-text" #content>{{ card.description }}</template>
        </Card>
        <Card v-else key="back" :class="{ active: card.isActive }" class="card">
            <template class="card-text" #content> {{ card.title }} </template>
        </Card>
      </Transition>
      </div>
    </div>
  </div>
</template>

<style scoped>

.cards-display {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}
.card-container{
  perspective: 1000px;
}

.card {
  position: relative;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: 10rem;
  height: 10rem;
  transition: transform 0.4s;
  backface-visibility: hidden;
  color: rgb(45, 45, 174);
  background-color: white;
  border-radius: 5px;
}
.active {
  color: white;
  background-color: rgb(45, 45, 174);
}

.card-flip-enter-from,
.card-flip-leave-to {
  transform: rotateX(180deg);
}
</style>
