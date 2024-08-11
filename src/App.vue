<template>
  <div class="menu">
    <a v-for="name in menus" :key="name">{{name}}</a>
  </div>
  <img alt="Vue logo" src="./assets/logo.png">
  <div v-for="(name, i) in products" :key="i">
    <h4>{{ name }}</h4>
    <p>{{ i * 10 }}</p>
    <button @click="repoertNumIncrease(i)">허위매물신고</button>
    <span>신고수 : {{ productsReportNum[i] }}</span>
  </div>
  <!-- <div>
    <h4>{{ products[0] }}</h4>
    <p>50 만원</p>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>70만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>70만원</p>
  </div> -->
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
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
    }
  },
}
</script>

<style>
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
</style>
