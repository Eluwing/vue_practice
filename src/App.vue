<template>
  <transition name="fade">
    <Modal @closeModal="toggleModal" :isOpenModal="isOpenModal" :room="oneRooms[modalClickedIndex]" />
  </transition>

  <div class="menu">
    <a v-for="name in menus" :key="name">{{ name }}</a>
  </div>
  <Discount v-if="isShowDiscount" />
  <SortSelectBox :sortItems="sortItems" @changeSelectdItem="handleSortChange" />
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
import SortSelectBox from "./components/SortSelectBox.vue";

export default {
  name: "App",
  data() {
    return {
      isShowDiscount: true,
      isOpenModal: false,
      modalClickedIndex: 0,
      products: ["板橋区ワンルーム", "足立区ワンルーム", "千代田区ワンルーム"],
      menus: ["Home", "Product", "About"],
      productsReportNum: [],
      oneRooms: data,
      sortItems: ["値段ごとにソート(昇順)", "値段ごとにソート(降順)", "物件名"],
    };
  },
  created() {
    //サーバーからデータ取得コード作成
  },
  mounted() {
    // 2秒後、Discountコンポーネント表示解除
    // setTimeout(() => {
    //   this.isShowDiscount = false;
    // }, 2000);
    this.productsReportNum = Array(this.oneRooms.length).fill(0);
    // 初期ソートを最初の文字列で設定
    this.handleSortChange(this.sortItems[0]);
  },
  components: {
    Discount,
    Modal,
    Card,
    SortSelectBox,
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
    priceAscSort() {
      this.oneRooms.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceDescSort() {
      this.oneRooms.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    nameSort() {
      this.oneRooms.sort(function (a, b) {
        // 英語小文字・大文字区分なし
        return a.title.localeCompare(b.title);
      });
    },
    handleSortChange(selectedItem) {
      switch (selectedItem) {
        case "値段ごとにソート(昇順)":
          this.priceAscSort();
          break;
        case "値段ごとにソート(降順)":
          this.priceDescSort();
          break;
        case "物件名":
          this.nameSort();
          break;
        default:
          break;
      }
    },
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
  opacity: 1;
  transform: translateY(0px);
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
