<template>
  <div>
    <label>Введите ваш логин (test):<input ref="inp" v-model="inputValue" type="text" /></label><br />
    <button @click="clearInp" class="button">Clear</button>
  </div>
</template>

<script>
import { dataMails } from "@/constans/arrMail.js";
export default {
  name: "inpMail",
  props: {
    emailVal: {
      type: String,
    },
    mailModifiers: {
      default: () => ({}),
    },
  },
  computed: {
    inputValue: {
      get() {
        return this.emailVal;
      },
      set(newVal) {
        const mailFind = dataMails.find((obj) => obj.userMail.toUpperCase() === newVal.toUpperCase());
        if (mailFind) {
          newVal = `${mailFind.userMail}@inv.mn.edu`;
        }
        this.$emit("update:emailVal", newVal);
        if (!mailFind) {
          this.$refs.inp.style.backgroundColor = "red";
        } else this.$refs.inp.style.backgroundColor = "white";
      },
    },
  },
  methods: {
    clearInp() {
      this.$nextTick(() => (this.$refs.inp.value = ""));
      this.$refs.inp.style.backgroundColor = "white";
    },
  },
};
</script>

<style lang="scss" scoped>
.error {
  background-color: red;
}
</style>
