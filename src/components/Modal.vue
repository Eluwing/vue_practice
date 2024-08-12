<template>
  <div class="black-bg" v-if="isOpenModal">
    <div class="white-bg">
      <h4>{{oneRooms[modalClickedIndex].title}}</h4>
      <p>{{oneRooms[modalClickedIndex].content}}</p>
      <p>{{ oneRooms[modalClickedIndex].price }} 万円</p>
      <!-- Fix me: 現在、動かない -->
      <!-- <button @click="toggleModal">戻る</button> -->
      <Discount/>
    </div>
  </div>
</template>

<script>
export default {
  name : 'ModalItem',
  props : {
    oneRooms : Array,
    isOpenModal : Boolean,
    modalClickedIndex : Number,

  }
}
</script>

<style>

</style>