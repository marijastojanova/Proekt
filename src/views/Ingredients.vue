<template>
<div class="p-8">
        <h1 class="text-4xl font-bold mb-4 text-orange-500 font-bold">Ingredients</h1>
        <input 
        type="text" 
        v-model="keyword"
        class="rounded border-2 bg-white border-gray-200 w-full mb-3" 
        placeholder="Search for Ingredients"
        @change="searchMeals"
        />
        
        <router-link 
        :to="{name:'byIngredient', params:{ingredient:ingredient.strIngredient}}" 
        v-for="ingredient of computedIngredients" 
        :key="ingredient.idIngredient" 
        class=" block bg-white rounded p-3 mb-3">
                <h3 class="text-2xl font-bold shadow mb-3">{{ ingredient.strIngredient }}</h3>
                <p>{{ ingredient.strDescription }}</p>
        </router-link>
</div>
</template>
<script setup >
import { onMounted, ref } from 'vue';
import {computed} from "@vue/reactivity"
import axiosClient from '../axiosClient';

const keyword=ref('')
const ingredients=ref([]);
const computedIngredients=computed(()=>{
        if(!computedIngredients) return ingredients;
        return ingredients.value.filter((i)=> i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase()));
});

onMounted(()=>
{
        axiosClient.get('list.php?i=list')
        .then(({data})=>
        {
                ingredients.value=data.meals

        })
}
)
</script>