<template>
  <div class="container-list">
    <product-item v-for="product in productsData" :key="product.id" :item-data="product" />
    <div class="empty-store" v-if="isEmpty">Список пуст</div>
  </div>
</template>

<script>
import productItem from "./productItem.vue";
export default {
  components: { productItem },
  name: "productsList",
  props: {
    productsData: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    isEmpty() {
      return this.productsData.length === 0;
    },
  },
};
</script>

<style lang="scss" scoped>
.container-list {
  border-block: 1px solid black;
  padding: 10px;
  display: grid;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  grid-column-gap: 20px;
  grid-row-gap: 20px;
}
</style>
