<template>
  <div id="app">
    <div class="rating-container">
      <RateBox v-model="rating" :editable="isEditable" />
      <p class="rating-text">Current Rating: {{ rating }}</p>
    </div>
    <button @click="toggleEditable" class="custom-btn">
      {{ isEditable ? 'Disable' : 'Enable' }} Editing
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import RateBox from './components/RateBox.vue';

const rating = ref(0);
const isEditable = ref(true);

const toggleEditable = () => {
  isEditable.value = !isEditable.value;
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.rating-container {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.rating-text {
  margin-left: 10px;
  font-size: 18px;
}

.custom-btn {
  background-color: #ff5722;
  color: white; 
  border: none; 
  border-radius: 50px;
  padding: 12px 24px; 
  font-size: 16px; 
  cursor: pointer; 
  transition: background-color 0.3s;
}

.custom-btn:hover {
  background-color: #e64a19;
}
</style>
