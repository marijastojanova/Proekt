<template>
<div>
    <h1 class="text-4xl font-bold mb-4 mt-8 ml-8 text-orange-500 font-bold ">Search Meals By Letter </h1>
        <div class="flex justify-center gap-2 mt-2">
        <router-link :to="{name: 'byLetter', params:{letter}}" v-for="letter in letters"
         :key="letter">
            {{ letter }}
        </router-link>
    </div>
    <Meals :meals="meals"/>
</div>
</template>
<script setup >
import { onMounted, watch } from 'vue';
import store from '../store';
import { useRoute } from 'vue-router';
import { computed } from '@vue/reactivity';
import MealItem from '../components/MealItem.vue'
import Meals from '../components/Meals.vue'


const route=useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
const meals=computed(()=>store.state.mealsByLetter)

watch(route,()=>
{
    store.dispatch('searchMealsByLetter', route.params.letter)

})

onMounted(() =>{
    store.dispatch('searchMealsByLetter', route.params.letter)
})
</script>