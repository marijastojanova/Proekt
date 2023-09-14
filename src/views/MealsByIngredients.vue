<template>
        <Meals :meals="meals"/>
</template>
<script setup >
import { computed, onMounted, ref } from 'vue';
import store from '../store';
import { useRoute } from 'vue-router';
import Meals from '../components/Meals.vue'
import axiosClient from '../axiosClient';

const route=useRoute();
const meals=computed(()=>store.state.mealsByIngredient)
const ingredients=ref([])
onMounted(()=>{
        store.dispatch('searchMealsByIngredient',route.params.ingredient)
})
</script>