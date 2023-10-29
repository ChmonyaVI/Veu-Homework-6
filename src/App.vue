<template>
  Задача №1<br />
  <first-task title="Введите возраст:" v-model:ageVal.check.setColor="ageValue" />
  <div>{{ ageValue }}</div
  ><br /><br /><br />
  Задача №2
  <br />
  <second-task title="Введите путь или название JS файла:" v-model:textVal.checkPath="textJSValue" /><br /><br /><br />
  Задача №3<br />
  <inp-mail v-model:emailVal.check="inputValue" /><br /><br /><br />
  Задача №4<br />
  <check-info-user
    v-model:ageVal.checkAge="ageValueTask4"
    v-model:nameVal.checkName="nameValueTask4"
  /><br /><br /><br />
  Задача №5<br />
  <div class="container-task5">
    <products-filter v-model:brand.checkBrand="brandVal" v-model:seller.checkSeller="sellerVal" />
    <products-list :products-data="filteredItemList" />
  </div>
</template>

<script>
//Задача №1
import FirstTask from "./components/task1/FirstTask.vue";
//Задача №2
import SecondTask from "./components/task2/SecondTask.vue";
//Задача №3
import InpMail from "./components/task3/inpMail.vue";
//Задача №4
import CheckInfoUser from "./components/task4/checkInfoUser.vue";
//Задача №5
import ProductsList from "./components/task5/productsList.vue";
import ProductsFilter from "./components/task5/productsFilter.vue";
import { notebooksList } from "@/constans/dataStore.js";

export default {
  name: "App",

  components: {
    InpMail,
    CheckInfoUser,
    FirstTask,
    SecondTask,
    ProductsFilter,
    ProductsList,
  },

  data() {
    return {
      ageValue: null,
      textJSValue: null,
      inputValue: null,
      nameValueTask4: null,
      ageValueTask4: null,
      notebooksList,
      brandVal: "Выберете бренд",
      sellerVal: "Выберете продавца",
    };
  },
  computed: {
    filteredItemList() {
      const defaultBrandSelect = this.brandVal === "Выберете бренд";
      const defaultSellerSelect = this.sellerVal === "Выберете продавца";
      if (defaultBrandSelect && defaultSellerSelect) return notebooksList;
      if (!defaultBrandSelect && !defaultSellerSelect && this.brandVal && this.sellerVal) {
        return notebooksList.filter(
          (notebook) => notebook.brand === this.brandVal && notebook.seller === this.sellerVal
        );
      }
      if (this.brandVal && defaultSellerSelect)
        return notebooksList.filter((notebook) => notebook.brand === this.brandVal);
      if (this.sellerVal && defaultBrandSelect)
        return notebooksList.filter((notebook) => notebook.seller === this.sellerVal);
      return notebooksList;
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/index.scss";
.container-task5 {
  display: flex;
}
</style>
