<template>
  <div>
    <button @click="toggleFavorites" :style="buttonStyle" :disabled="false"
      class="px-3 py-2 rounded border-2 text-white transition-colors">
      Favorite
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import store from '../store'; 



const buttonStyle = {
  backgroundColor: 'lightblue',
};



function toggleFavorites() {
  
  store.dispatch('toggleFavorite', meal.value);
}
const { meal } = defineProps({
  meal: {
    type: Array,
    default: () => [],
  },
});
</script>