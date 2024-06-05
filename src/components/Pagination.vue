<template>
  <div class="container">
    <div class="pagination">
      <button @click="$emit('prev-page')" :disabled="!prev">Prev</button>
      <button @click="$emit('next-page')" :disabled="!next">Next</button>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  prev: {
    type: String,
    required: false,
  },
  next: {
    type: String,
    required: false,
  },
});
</script>

<style scoped>
.container{
width: 100vw;
display: flex;
justify-content: center;
padding-bottom: 100px;
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
  background-color: rgba(132, 42, 210, 0.7);
  color: white;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s;
}

button:hover:not(:disabled) {
  background-color: rgba(132, 42, 210);
  transform: scale(1.05);
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
