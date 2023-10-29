<template>
  <div>
    <label
      >{{ title }} <input ref="inp" v-model="textFromUser" type="text" />
      <button @click="clearInp" class="button">Clear</button></label
    >
  </div>
</template>

<script>
export default {
  name: "SecondTask",
  props: {
    title: {
      type: String,
      default: "",
    },
    textVal: {
      type: String,
    },
    textValModifiers: {
      default: () => ({}),
    },
  },

  computed: {
    textFromUser: {
      get() {
        return this.textVal;
      },
      set(val) {
        let result = this.getRegExp(val);
        if (result) {
          val = String(val.match(/\w+\.js/g));
        }
        this.$emit("update:textVal", val);
        if (val && this.textValModifiers.checkPath) this.setBGColor(val);
      },
    },
  },
  methods: {
    setBGColor(val) {
      let result = this.getRegExp(val);
      if (!result) this.$refs.inp.style.backgroundColor = "red";
      else this.$refs.inp.style.backgroundColor = "green";
    },
    getRegExp(val) {
      return /\w+\.js/g.test(val);
    },
    clearInp() {
      this.$nextTick(() => (this.$refs.inp.value = ""));
      this.$refs.inp.style.backgroundColor = "white";
    },
  },
};
</script>

<style lang="scss" scoped></style>
