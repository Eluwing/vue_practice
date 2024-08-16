<template>
    <label>Select an item:</label>
    <!-- Warning: selectboxの値が変更された場合実行される
     change属性をカスタマイズが必要なためv-model利用禁止 -->
    <select :value="selectedItem" @change="handleChange">
      <option v-for="(item) in sortItems" :key="item" :value="item">
        {{ item }}
      </option>
    </select>
    <p v-if="selectedItem">You selected: {{ selectedItem }}</p>
</template>

<script>
export default {
  name: 'SortSelectBoxItem',
  props: {
    sortItems: Array,
  },
  data(){
    return{
      selectedItem: "",
    }
  },
  emits: ['changeSelectdItem'],
  methods: {
    handleChange(event) {
      this.selectedItem = event.target.value;
      this.$emit('changeSelectdItem', this.selectedItem)
    },
  }
};
</script>

<style>
</style>