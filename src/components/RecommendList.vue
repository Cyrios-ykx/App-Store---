<script setup lang="ts">
import topGrossingApplications from '../assets/topGrossingApplications.json'
</script>

<template>
<div class="list-container">
    <div>Recommend</div>
    <div class="list-layout">
              <div v-for="item of topGrossingApplications.feed.entry" :key="item.id.attributes['im:id']" class="applications-layout">
                <div><img :src="item['im:image'][1].label" alt=""></div>
            <div>
                <div class="applications-text">{{item['im:name'].label}}</div>
                <div class="applications-text applications-category">{{item['category'].attributes.label}}</div>
            </div>
            </div>
        
    </div>
</div>
</template>

<style scoped>
.list-container{
    padding: 10px 15px;
    border-top: 1px rgb(225, 225, 225) solid;
    border-bottom: 1px rgb(225, 225, 225) solid;
    overflow: hidden;
}
.list-layout{
    display: flex;
    width: 100vw;
    overflow: scroll;
}
.applications-layout{
    width: 75px;
    margin-right: 10px;
}
.applications-layout:last-child{
    margin-right: 25px;
}
.applications-layout img{
    border-radius: 20%;
    margin: 10px 0;
}
.applications-text{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: center;
}
.applications-category{
    color: gray;
    font-size: 12px;
}

</style>
