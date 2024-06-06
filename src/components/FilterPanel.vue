<template>
  <div class="filter">
    <div class="filter-header">
      <h2>Rick and Morty API</h2>
    </div>
    <div class="flex-row">
      <div class="section">
        <h3>Name</h3>
        <div class="inputbox">
          <input v-model="name" type="text" placeholder="Search Character">
        </div>
      </div>
      <div class="section">
        <h3>Status</h3>
        <div class="custom-select">
          <select v-model="status">
            <option value="">All</option>
            <option value="alive">Alive</option>
            <option value="dead">Dead</option>
            <option value="unknown">Unknown</option>
          </select>
        </div>
      </div>
    </div>
    <div class="btn-container">
      <button class="search-btn" @click="handleSearch">Search</button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const name = ref('');
const status = ref('');

const emit = defineEmits(['update:name', 'update:status'])

const handleSearch = () => {
  emit('update:name', name.value);
  emit('update:status', status.value === 'all' ? '' : status.value);
};
</script>

<style scoped>
.filter {
  max-width: 56vw;
  background: linear-gradient(to bottom, rgba(245, 245, 245, 0.9), rgba(245, 245, 245));
  filter: drop-shadow(2px 2px 6px rgba(0, 0, 0, 0.25));
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  justify-content: center;
}

.filter-header {
  color: whitesmoke;
  background: linear-gradient(135deg, #444, #333);
  text-align: center;
  padding: 18px 24px;
  box-shadow: inset -3px 2px 6px rgba(255, 248, 170, 0.18);
}

.filter-header h2 {
  font-size: 2rem;
  margin: 0;
}

.flex-row {
  display: flex;
  justify-content: space-between;
  align-items: flex-start; 
  flex-direction: row;
  padding: 0 2vw;
  gap: 3vw
}

.section {
  flex: 1;
  padding: 4vh 0;
  display: flex;
  flex-direction: column;
}

h3 {
  margin: 0 0 10px;
  color: #444;
  font-size: 1.8rem;
}

.inputbox {
  position: relative;
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  gap: 10px;
}

.inputbox input {
  width: 100%;
  padding: 10px;
  border: 2px solid rgba(200, 40, 150, 0.8);
  border-radius: 5px;
  background: transparent;
  outline: none;
  color: #23242a;
  font-size: 1.2rem;
  letter-spacing: 0.05em;
}

.btn-container{
  display: flex;
  justify-content: center;
  padding: 0 2vw;
}

.search-btn{
  margin-bottom: 3vh;
 width: 100%;
 font-size: 1rem;
 color: whitesmoke;
 padding: 12px; 
 border-radius: 5px;
 border: none;
 background: rgba(60, 60, 60);
}

.search-btn:hover{
 background: rgba(60, 60, 60, 0.8);
}

.custom-select {
  position: relative;
}

.custom-select:hover select {
  background-color: rgba(200, 40, 150, 0.8);
}

.custom-select select {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 5px;
  background-color: rgb(200, 40, 150);
  color: whitesmoke;
  font-size: 1.2rem;
  font-weight: 400;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  letter-spacing: 0.05em;
}

select option {
  background-color: white;
  color: #444;
  font-size: 1.4rem;
}
</style>
