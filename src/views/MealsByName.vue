<template>
<div class="p-8 pb-0">
        <h1 class="text-4xl font-bold mb-4 text-orange-500 font-bold ">Search Meals </h1>
        <input 
        type="text" 
        v-model="keyword"
        class="rounded border-2 bg-white border-gray-200 w-full" 
        placeholder="Search for Meals"
        @change="searchMeals"
        />
</div>
<Meals :meals="meals"/>
</template>
<script setup >
import {ref, onMounted} from "vue";
import store from '../store';
import {computed} from '@vue/reactivity';
import {useRoute} from "vue-router"
import MealItem from '../components/MealItem.vue'
import YoutubeButton from '../components/YoutubeButton.vue'
import Meals from '../components/Meals.vue'

const route=useRoute();
const keyword=ref("");
const meals=computed(()=> store.state.searchedMeals)
function searchMeals(){
        if(keyword.value){
                store.dispatch('searchMeals',keyword.value);
        }else{
                store.commit('setSearchedMeals',[]);
        }
}
onMounted(()=>{
        keyword.value=route.params.name
        if(keyword.value){
                searchMeals()
        }
}

)
</script>