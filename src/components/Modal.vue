<template>
  <div class="black-bg" v-if="isOpenModal">
    <div class="white-bg">
      <h4>{{ room.title }}</h4>
      <p>{{ room.content }}</p>
      <!-- inputからデータ受ける方法：@input、v-model利用 -->
      <!-- <input @input = "month = $event.target.value" /> -->
      <input v-model="month" />
      <p>{{ month }}ヶ月選択 : {{ room.price * month }} 万円</p>
      <button @click="$emit('closeModal')">戻る</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalItem",
  data() {
    return {
      month: 0,
    }
  },
  // life cycelを利用してバリデーションチェック
  updated() {
    if (this.month == 2) {
      alert("2入力は禁止です");
      this.month = 1;
    }
  },
  // バリデーションチェック
  watch: {
    month(input) {
      const pattern = /\D/;

      if (pattern.test(input)) {
        alert("数値のみ入力可能です。");
        this.month = 1;
      }
    },
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
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
</style>