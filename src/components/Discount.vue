<template>
  <div class="discount">
    <h4>今新規登録すると{{salePercent}}%割り引き</h4>
  </div>
</template>

<script>
export default {
  name: 'DiscountItem',
  data() {
    return {
      salePercent: 30,
    }
  },
  mounted() {
    const salePercnetDesent = setInterval(() => {
      if (this.salePercent > 0) {
        this.salePercent -= 1;
      } else {
        clearInterval(salePercnetDesent); // パーセンテージが0になった場合、Interval中止
      }
    }, 1000); // 1秒ごとに実行
  }
}
</script>

<style>
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>