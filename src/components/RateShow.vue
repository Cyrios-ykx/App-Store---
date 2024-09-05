<template>
  <div class="wrapper">
    <div class="stars">
      <div v-for='(star,index) in 5'>
        <span class="star-off star" :style="{background:'url(' + starOffImg + ')'}"></span>
        <span class="star-on star" :style='{width:(index < Number(data.rate) ?"100":"0")+ "%",background:"url(" + starOnImg + ")"}' v-if='index < parseInt(data.rate) '></span>
        <span class="star-on star" :style='{width:(index == Math.ceil(Number(data.rate)) - 1 ? 100 * Number("0." + data.rate.split(".")[1]):"0")+ "%",background:"url(" + starOnImg + ")"}' v-else></span>
      </div>
    </div>
    <div class="custom-text">({{ data.count }})</div>
  </div>
</template>

<script setup lang="ts">
import starOnImg from '../assets/img/on.png'
import starOffImg from '../assets/img/off.png'

defineProps<{ data: {
  rate: string,
  count: string
}}>()
</script>

<style scoped>
.wrapper{
  display: flex;
  align-items: center;
}
.wrapper .stars{
  display: flex;
  align-items: center;
}
.wrapper .stars>div{
  position: relative;
  width: 8px;
  height: 8px;
  display: inline-block;
}
.wrapper .star{
  position: absolute;
  width: 8px;
  height: 8px;
  background-repeat: no-repeat !important;
  background-size: cover !important;
}
.custom-text{
  margin-left: 5px;
  color: gray;
  font-size: 10px;
}
</style>
