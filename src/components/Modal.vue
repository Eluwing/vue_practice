<template>
  <div class="white-bg">
    <h4>{{ room.title }}</h4>
    <p>{{ room.content }}</p>
    <p>{{ room.price }} 万円</p>
    <button @click="$emit('closeModal')">戻る</button>
  </div>
</template>

<script>
export default {
  name: "ModalItem",
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