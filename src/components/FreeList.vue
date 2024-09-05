<script setup lang="ts">
import { ref, watch } from 'vue';
import topFreeApplications from '../assets/topFreeApplications.json'
import topFreeApplicationsLookup from '../assets/topFreeApplicationsLookup.json'
import RateShow from '../components/RateShow.vue'

const props = defineProps<{ keyword: string}>()

const lookupMap = new Map()

topFreeApplicationsLookup.results.forEach(result=>{
    lookupMap.set(result.trackId, result)
})

const getUserRating = (trackId: number)=>{
    const trackItem = lookupMap.get(trackId)
    const rate = trackItem?.averageUserRatingForCurrentVersion ?? trackItem?.userRatingCount 
    const count = trackItem?.userRatingCountForCurrentVersion ?? trackItem?.userRatingCount 
    return {
        rate: String(rate),
        count: String(count)
    }
}

const freeList = ref([])
freeList.value = topFreeApplications.feed.entry

watch(
    ()=>props.keyword,
    (newVal)=>{
        if (newVal) {
            freeList.value = topFreeApplications.feed.entry.filter(item=> item['im:name'].label.toLocaleLowerCase().includes(newVal.toLocaleLowerCase()))
        } else {
            freeList.value = topFreeApplications.feed.entry
        }
})
</script>

<template>
    <div class="application-list">
        <div v-for="(item ,index) of freeList" :key="item.id.attributes['im:id']" class="application-row">
            <div class="custom-text">{{ index + 1 }}</div>
            <div><img :src="item['im:image'][0].label" alt=""></div>
            <div>
                <div>{{item['im:name'].label}}</div>
                <div class="custom-text">{{item['category'].attributes.label}}</div>
                <div class="application-lookup-container">
                    <RateShow :data="getUserRating(Number(item.id.attributes['im:id']))"></RateShow>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.custom-text{
    color: gray;
    font-size: 12px;
}
.application-list{
    display: flex;
    flex-direction: column;
}
.application-row{
    padding: 10px;
    display: flex;
    gap: 10px;
    align-items: center;
    margin-left: 15px;
    border-bottom: 1px rgb(225, 225, 225) solid;
}
.application-row:nth-child(n)  img {
    border-radius: 20%;
}
.application-row:nth-child(2n)  img {
    border-radius: 50%;
}
.application-row:last-child{
    border-bottom: none;
}
.application-lookup-container{
    display: flex;
}
</style>
