<template>
  <Modal :oneRooms = "oneRooms" :isOpenModal = "isOpenModal" :modalClickedIndex = "modalClickedIndex"/>
  <div class="menu">
    <a v-for="name in menus" :key="name">{{name}}</a>
  </div>
  <Discount/>

  <img alt="Vue logo" src="./assets/logo.png">
  <div v-for="(room,i) in oneRooms" :key="i">
    <Card :room = "room" :cardKey = "i" :productsReportNum = "productsReportNum[i]"/>
  </div>
</template>

<script>

import data from './assets/oneroom.js'
import Discount from './components/Discount.vue'
import Modal from './components/Modal.vue'
import Card from './components/Card.vue'

export default {
  name: 'App',
  data(){
    return{
      isOpenModal : false,
      modalClickedIndex: 0,
      products : ['板橋区ワンルーム', '足立区ワンルーム', '千代田区ワンルーム'],
      menus : ['Home', 'Product', 'About'],
      productsReportNum : [],
      oneRooms : data,
    }
  },
  mounted() {
    this.productsReportNum = Array(this.products.length).fill(0)
  },
  components: {
    Discount,
    Modal,
    Card,
  },
  methods : {
    repoertNumIncrease(index){
      this.productsReportNum[index] += 1
    },
    toggleModal(){
      this.isOpenModal = !this.isOpenModal
    },
    setModalClickedIndex(clickedIndex){
      this.modalClickedIndex = clickedIndex
    },
    roomTitleClick(clickedIndex){
      this.toggleModal()
      this.setModalClickedIndex(clickedIndex)
    },
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
