<template>
  <keep-alive>
  <div class="card" @mouseover="isHovered = true" @mouseleave="isHovered = false">
        <img :src="card.image" alt="card.name"/>
      <div class="card-info" :class="{ 'show-info': isHovered }">
        <h2>{{ card.name }}</h2>
        <p>{{ card.status }}</p>
        <p>{{ card.gender }}</p>
        <p>Origin: {{ card.origin.name }}</p>
      </div>
    </div>
  </keep-alive>
</template>

<script setup>
import { defineProps, ref } from 'vue';

const props = defineProps({
  card: {
    type: Object,
    required: true,
  },
});

const isHovered = ref(false)
</script>

<style scoped>
.card {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  width: 100%;
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

.card img {
  width: 100%;
  height: 100%;
  display: block;
  border-radius: 8px;
  object-fit: cover;
  transition: opacity 0.3s ease-in-out;
}

.card-info {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 16px;
  box-sizing: border-box;
  transform: translateY(100%);
  transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out;
  opacity: 0;
  border-radius: 0 0 8px 8px;
}

.card:hover .card-info {
  transform: translateY(0);
  opacity: 1;
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
}

.show-info {
  transform: translateY(0);
  opacity: 1;
}
</style>
