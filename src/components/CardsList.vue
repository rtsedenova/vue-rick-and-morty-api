<template>
    <div >
      <div class="cards-list" v-if="all">
        <Card v-for="card in cards" :key="card.id" :card="card" />
      </div>
      <div class="cards-list" v-else>
        <Card v-for="card in filteredCards" :key="card.id" :card="card" />
      </div>
    </div>
    <Pagination class="pagination" :prev="paginationInfo.prev" :next="paginationInfo.next" @prev-page="fetchPrevPage" @next-page="fetchNextPage"
    :total-pages="totalPages" :current-page="currentPage"/>
</template>

<script setup>
import { ref, onMounted, defineProps, defineExpose, watch } from 'vue';
import Card from './Card.vue';
import Pagination from './Pagination.vue';

const cardsPerPage = 20;

const cards = ref([]);
const paginationInfo = ref({ prev: null, next: null });
const filteredCards = ref([]);

const totalPages = ref(null)
const currentPage = ref(1)

const all = ref(true);

const initialUrl = 'https://rickandmortyapi.com/api/character/';

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  status:{ type: String,
    required: true
  }
});

async function fetchData(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    cards.value = data.results;
    paginationInfo.value = {
      prev: data.info.prev,
      next: data.info.next,
    }
    filterCards();
  } catch (error) {
    console.error('Failed to fetch data:', error);
  }
}

onMounted(() => {
  fetchData(initialUrl);
});

function fetchPrevPage() {
  if (paginationInfo.value.prev) {
    fetchData(paginationInfo.value.prev);
  }
}

function fetchNextPage() {
  if (paginationInfo.value.next) {
    fetchData(paginationInfo.value.next);
  }
}

function filterCards() {
  if (props.name || props.status) {
    filteredCards.value = cards.value.filter(card => {
      const nameMatch = !props.name || card.name.toLowerCase().includes(props.name.toLowerCase());
      const statusMatch = !props.status || card.status.toLowerCase() === props.status.toLowerCase();
      return nameMatch && statusMatch;
    });
    all.value = false;
  } else {
    filteredCards.value = [];
    all.value = true;
  }
  totalPages.value = setTotalPages(); 
}

watch(() => [props.name, props.status], () => {
  fetchData(`${initialUrl}?name=${props.name}&status=${props.status}`); 
});

function setTotalPages() {
  return Math.ceil(filteredCards.value.length / cardsPerPage.value);
}

function paginatedCards() {
  const startIndex = (currentPage.value - 1) * cardsPerPage.value;
  const endIndex = startIndex + cardsPerPage.value;
  return filteredCards.value.slice(startIndex, endIndex);
}
</script>

<style scoped>
.cards-list{
  padding: 0 2vw;
  padding-top: 26vh;
  padding-bottom: 14vh;
  display: grid;
  grid-template-columns: repeat(2, minmax(200px, 1fr));
  gap: 10px;
}

@media screen and (min-width: 768px) {
  .cards-list{
    grid-template-columns: repeat(3, minmax(200px, 1fr));
    gap: 12px;
  }
}

@media screen and (min-width: 1024px) {
  .cards-list{
    grid-template-columns: repeat(4, minmax(200px, 1fr));
    gap: 14px;
  }
}

.pagination {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

button {
  margin: 0 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #e50914;
  color: white;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s;
}

button:hover:not(:disabled) {
  background-color: #f40612;
  transform: scale(1.05);
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
