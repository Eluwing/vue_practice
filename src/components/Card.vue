<template>
  <div :key="room.id">
    <img :src="room.image" class="room-img">
    <h4 @click="$emit('openModal',room.id)">{{ room.title }}</h4>
    <h4>{{ room.price }}万円</h4>
    <button @click="$emit('reportNumIncrease',room.id)">虚偽物件報告</button>
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