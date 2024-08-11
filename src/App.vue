<template>
  <div class="black-bg" v-if="isOpenModal">
    <div class="white-bg">
      <h4>詳細なページタイトル</h4>
      <p>詳細内容記載</p>
      <button @click="toggleModal">戻る</button>
    </div>
  </div>
  <div class="menu">
    <a v-for="name in menus" :key="name">{{name}}</a>
  </div>
  <img alt="Vue logo" src="./assets/logo.png">
  <div v-for="(name, i) in products" :key="i">
    <img :src="`/room${i}.jpg`" class="room-img">
    <h4 @click="toggleModal">{{ name }}</h4>
    <p>{{ i * 10 }} 万円</p>
    <button @click="repoertNumIncrease(i)">虚偽物件報告</button>
    <span>報告数 : {{ productsReportNum[i] }}</span>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      isOpenModal : false,
      products : ['板橋区ワンルーム', '足立区ワンルーム', '千代田区ワンルーム'],
      menus : ['Home', 'Product', 'About'],
      productsReportNum : [],
    }
  },
  mounted() {
    this.productsReportNum = Array(this.products.length).fill(0)
  },
  components: {
  },
  methods : {
    repoertNumIncrease(index){
      this.productsReportNum[index] += 1
    },
    toggleModal(){
      this.isOpenModal = !this.isOpenModal
    }
  },
}
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img {
  width: 100%;
  max-width: 820px;
  max-height: 312px;
  margin-top: 40px;
}
</style>
