<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4">Favorite</h1>
    <Meals :meals="favoriteMeals" />
  </div>
</template>

<script setup>
import { computed, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { mapState } from 'vuex';
import store from "../store"
import Meals from '../components/Meals.vue';

const route = useRoute();
const favoriteMeals = computed(() => store.state.favorites);
onMounted(() =>{
    store.dispatch('toggleFavorite', route.params.favorite)
})
</script> 