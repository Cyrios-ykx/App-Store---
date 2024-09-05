<script setup lang="ts">
import { ref } from 'vue'
import FreeList from "../components/FreeList.vue";
import RecommendList from "../components/RecommendList.vue";
import SearchBanner from "../components/SearchBanner.vue";

const keyword = ref('')
const handleSearch = (value: string)=>{
    keyword.value = value
}
</script>

<template>
  <div>
    <search-banner @change="handleSearch"/>
    <recommend-list/>
    <free-list :keyword="keyword"/>
  </div>
</template>

<style scoped>
</style>
