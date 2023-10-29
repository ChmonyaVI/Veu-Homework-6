<template>
  <div class="container">
    <label
      >Имя пользователя: <input ref="inpName" v-model="nameUser" type="text" style="background-color: red"
    /></label>
    <label>Возраст пользователя: <input ref="inpAge" v-model="valueAge" type="Number" /></label>
    <button @click="clearInp" class="button">Clear</button>
  </div>
</template>

<script>
export default {
  name: "checkInfoUser",
  props: {
    nameVal: {
      type: String,
      default: "",
    },
    ageVal: {
      type: Number,
      default: null,
    },
    infoValModifiers: {
      default: () => ({}),
    },
  },
  computed: {
    nameUser: {
      get() {
        return this.nameVal;
      },
      set(val) {
        this.checkName(val);
        this.$emit("update:nameVal", val);
      },
    },
    valueAge: {
      get() {
        return this.ageVal;
      },
      set(val) {
        this.checkAge(val);
        this.$emit("update:ageVal", val);
      },
    },
  },
  methods: {
    checkAge(val) {
      if (val < 18) {
        this.$refs.inpAge.style.backgroundColor = "red";
      } else this.$refs.inpAge.style.backgroundColor = "green";
    },
    checkName(val) {
      if (val) {
        this.$refs.inpName.style.backgroundColor = "white";
      } else this.$refs.inpName.style.backgroundColor = "green";
    },
    clearInp() {
      this.$nextTick(() => (this.$refs.inpName.value = ""));
      this.$nextTick(() => (this.$refs.inpAge.value = ""));
      this.$refs.inpName.style.backgroundColor = "red";
      this.$refs.inpAge.style.backgroundColor = "white";
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 15px;
}
.button {
  width: 100px;
}
</style>
