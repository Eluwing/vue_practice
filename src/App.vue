<template>
  <transition name="fade">
    <div class="black-bg" v-if="isOpenModal">
      <Modal @closeModal="toggleModal" :room="oneRooms[modalClickedIndex]" />
    </div>
  </transition>

  <div class="menu">
    <a v-for="name in menus" :key="name">{{ name }}</a>
  </div>
  <Discount />
  <div>
    <label>Select an item:</label>
    <select v-model="selectedItem" @change="handleSortChange">
      <option v-for="(item, index) in sortItems" :key="index" :value="item">
        {{ item }}
      </option>
    </select>
    <p v-if="selectedItem">You selected: {{ selectedItem }}</p>
  </div>
  <button @click="priceAscSort">値段ごとにソート(昇順)</button>
  <button @click="priceDescSort">値段ごとにソート(降順)</button>
  <button @click="nameSort">名前ごとにソート</button>

  <img alt="Vue logo" src="./assets/logo.png" />
  <div v-for="(room, i) in oneRooms" :key="i">
    <Card
      @openModal="roomTitleClick"
      @reportNumIncrease="repoertNumIncrease"
      :room="room"
      :productsReportNum="productsReportNum[i]"
    />
  </div>
</template>

<script>
import data from "./assets/oneroom.js";
import Discount from "./components/Discount.vue";
import Modal from "./components/Modal.vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  data() {
    return {
      isOpenModal: false,
      modalClickedIndex: 0,
      products: ["板橋区ワンルーム", "足立区ワンルーム", "千代田区ワンルーム"],
      menus: ["Home", "Product", "About"],
      productsReportNum: [],
      oneRooms: data,
      sortItems: ["値段ごとにソート(昇順)","値段ごとにソート(降順)","物件名"],
      selectedItem: "",
    };
  },
  mounted() {
    this.productsReportNum = Array(this.oneRooms.length).fill(0);
    this.selectedItem = this.sortItems[0];
    this.handleSortChange();
  },
  components: {
    Discount,
    Modal,
    Card,
  },
  methods: {
    repoertNumIncrease(index) {
      this.productsReportNum[index] += 1;
    },
    toggleModal() {
      this.isOpenModal = !this.isOpenModal;
    },
    setModalClickedIndex(clickedIndex) {
      this.modalClickedIndex = clickedIndex;
    },
    roomTitleClick(clickedIndex) {
      this.toggleModal();
      this.setModalClickedIndex(clickedIndex);
    },
    priceAscSort(){
      this.oneRooms.sort(function(a,b){
        return a.price - b.price
      })
    },
    priceDescSort(){
      this.oneRooms.sort(function(a,b){
        return b.price - a.price
      })
    },
    nameSort(){
      this.oneRooms.sort(function(a,b){
        // 英語小文字・大文字区分なし
        return a.title.localeCompare(b.title)
      })
    },
    handleSortChange(){
      switch (this.selectedItem) {
        case "値段ごとにソート(昇順)" :
          this.priceAscSort()
          break
        case "値段ごとにソート(降順)" :
          this.priceDescSort()
          break
        case "物件名" :
          this.nameSort()
          break
        default :
          break
      }


    }
  },
};
</script>

<style>
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;transform: translateY(0px);
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}
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
