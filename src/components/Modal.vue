<template>
  <div class="white-bg">
    <h4>{{ room.title }}</h4>
    <p>{{ room.content }}</p>
    <!-- inputからデータ受ける方法：@input、v-model利用 -->
    <!-- <input @input = "month = $event.target.value" /> -->
    <input v-model.number="month" />
    <p>{{ month }}ヶ月選択 : {{ room.price * month }} 万円</p>
    <button @click="$emit('closeModal')">戻る</button>
  </div>
</template>

<script>
export default {
  name: "ModalItem",
  data(){
    return {
      month: 0,
    }
  },
  props: {
    room: Object,
    isOpenModal: Boolean,
    modalClickedIndex: Number,
  },
};
</script>

<style>
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>