<template>
  <div :key="room.id">
    <img :src="room.image" class="room-img">
    <h4 @click="$emit('openModal',room.id)">{{ room.title }}</h4>
    <!-- Fix me: 現在、コンポーネント化により@clickが動かない -->
    <!-- <button @click="repoertNumIncrease(i)">虚偽物件報告</button> -->
    <span>報告数 : {{ productsReportNum }}</span>
  </div>
</template>

<script>
export default {
  name : 'CardItem',
  props : {
    room : Object,
    productsReportNum : Number,
    cardKey : Number,
  },
}
</script>

<style>

</style>