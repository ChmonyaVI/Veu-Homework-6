<template>
  <div class="container-filter">
    <label class="label-brands"
      >Brands
      <select class="sorted-brands select-default" ref="brand" v-model="brandVal">
        <option selected>Выберете бренд</option>
        <option v-for="brand in brandsList" :key="brand" :value="brand">{{ brand }}</option>
      </select>
    </label>
    <br />
    <label class="label-brands"
      >Seller
      <select class="sorted-sellers select-default" ref="seller" v-model="sellerVal">
        <option selected>Выберете продавца</option>
        <option v-for="seller in sellersList" :key="seller" :value="seller">{{ seller }}</option>
      </select>
    </label>
  </div>
</template>

<script>
import { notebooksList } from "@/constans/dataStore.js";
export default {
  name: "productsFilter",
  props: {
    brand: {
      type: String,
    },
    brandModifiers: { default: () => ({}) },
    seller: {
      type: String,
    },
    sellerModifiers: { default: () => ({}) },
  },
  computed: {
    brandVal: {
      get() {
        return this.brand;
      },
      set(val) {
        if (this.brandModifiers.checkBrand) this.setBrandBGColor(val);
        this.$emit("update:brand", val);
      },
    },
    sellerVal: {
      get() {
        return this.seller;
      },
      set(val) {
        if (this.sellerModifiers.checkSeller) this.setSellerBGColor(val);
        this.$emit("update:seller", val);
      },
    },
    brandsList() {
      const brandsArr = [];
      notebooksList.map((notebook) => brandsArr.push(notebook.brand));
      const uniqBrands = this.getUniqArr(brandsArr);
      return uniqBrands;
    },
    sellersList() {
      const sellersArr = [];
      notebooksList.map((notebook) => sellersArr.push(notebook.seller));
      const uniqSellers = this.getUniqArr(sellersArr);
      return uniqSellers;
    },
  },
  methods: {
    getUniqArr(arr) {
      return [...new Set(arr)].sort();
    },
    setBrandBGColor(val) {
      if (val === "Выберете бренд") this.$refs.brand.style.backgroundColor = "green";
      else this.$refs.brand.style.backgroundColor = "white";
    },
    setSellerBGColor(val) {
      if (val === "Выберете продавца") this.$refs.seller.style.backgroundColor = "green";
      else this.$refs.seller.style.backgroundColor = "white";
    },
  },
};
</script>

<style lang="scss" scoped>
.container-filter {
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  padding: 10px;
}
</style>
