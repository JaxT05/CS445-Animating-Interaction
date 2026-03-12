<script setup>
import Card from 'primevue/card'
import { ref } from 'vue';

let cards = ref([
  {
    id: 'a',
    cardImage: '/src/assets/cowboy-dog.jpg',
    isActive: false
  },
  {
    id: 'a',
    cardImage: '/src/assets/cowboy-dog.jpg',
    isActive: false,
  },
  {
    id: 'b',
    cardImage: '/src/assets/dapper-dog.jpg',
    isActive: false
  },
  {
    id: 'b',
    cardImage: '/src/assets/dapper-dog.jpg',
    isActive: false
  },
  {
    id: 'c',
    cardImage: '/src/assets/propeller-dog.jpg',
    isActive: false
  },
  {
    id: 'c',
    cardImage: '/src/assets/propeller-dog.jpg',
    isActive: false
  },
  {
    id: 'd',
    cardImage: '/src/assets/strawberry-dog.webp',
    isActive: false
  },
  {
    id: 'd',
    cardImage: '/src/assets/strawberry-dog.webp',
    isActive: false
  }
]);

cards.value = cards.value.sort(() => Math.random() - 0.5);

const flippedCards = ref([]);
const amountMatches = ref(0);
const amountErrors = ref(0);

const handleCardClick = (card) => {
  if (card.isActive || flippedCards.value.length >= 2) {return} 
  else {
    card.isActive = true;
    flippedCards.value.push(card);
    if (flippedCards.value.length === 2) {
      if (flippedCards.value[0].id === flippedCards.value[1].id) {
        setTimeout(() => {
          cards.value = cards.value.filter(card => card.id !== flippedCards.value[0].id);
          cards.value = cards.value.filter(card => card.id !== flippedCards.value[1].id);
          amountMatches.value++;
          flippedCards.value = [];
        }, 1000);
      }
      else { 
        setTimeout(() => {
          flippedCards.value[0].isActive = false;
          flippedCards.value[1].isActive = false;
          amountErrors.value++;
          flippedCards.value = [];
        }, 1000);
      }
    }
  }
}
</script>

<template>
  <div class="score">
    <p>Matches: {{ amountMatches }}</p>
    <p>Failures: {{ amountErrors }}</p>
  </div>
  <div class="victory" v-if="cards.length === 0">Yay!</div>
  <div class="cards-display">
    <div v-for="card in cards" class="card-container">
      <div @click="handleCardClick(card)">
        <Transition name="card-flip" mode="out-in">
        <Card v-if="card.isActive" key="front" :class="{ active: card.isActive }" class="card">
            <template class="card-text" #content>
              <img :src="card.cardImage"/>
            </template>
        </Card>
        <Card v-else key="back" :class="{ active: card.isActive }" class="card">
        </Card>
      </Transition>
      </div>
    </div>
  </div>
</template>

<style scoped>
.victory {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 4rem;
}
.score {
  position: fixed;
  display: flex;
  flex-direction: row;
  gap: 1rem;
  top: 0;
  left: 0;
  margin: 4rem;
}

.cards-display {
  text-align: center;
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  place-items: center;
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
.card img {
  width: 100%;
  height: auto;
  aspect-ratio: 1/1;
  object-fit: cover;
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
