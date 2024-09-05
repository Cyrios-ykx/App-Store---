<script setup lang="ts">
import searchIcon from '../assets/svg/searchIcon.svg'

const emit = defineEmits<{
  (e: 'change', keyword: string): void
}>()

const handleSearch = (event: Event )=>{
    emit('change', (event.target as HTMLInputElement).value)
}
</script>

<template>
<div class="search-input-container align-center">
    <div class="search-icon-container align-center">
        <img :src="searchIcon" alt="" class="search-icon">
    </div>
    <input type="text" placeholder="Search..." class="search-input" @input="handleSearch">
</div>

</template>

<style scoped>
.align-center{
    display: flex;
    align-items: center;
}
.search-input-container{
    margin: 10px;
}
.search-icon-container {
    background-color: rgb(225, 225, 225);
    height: 32px;
    padding: 0 5px;
    border-radius: 10px 0 0 10px;
}
.search-icon{
    width: 16px;
}
.search-input{
    width: 100%;
    height: 32px;
    background-color: rgb(225, 225, 225);
    border: none;
    border-radius: 0 10px 10px 0;
}
</style>
