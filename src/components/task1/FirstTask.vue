<template>
  <div>
    <label class="label__age"
      >{{ title }}
      <input ref="inp" v-model="ageInfo" :key="updateKey" type="number" />
    </label>
    <template v-if="message">
      <div class="message">{{ message }}</div>
    </template>
  </div>
</template>

<script>
export default {
  name: "FirstTask",

  props: {
    title: {
      type: String,
      default: "",
    },
    ageVal: {
      type: Number,
    },
    ageValModifiers: {
      default: () => ({}),
    },
  },

  data() {
    return {
      updateKey: 0,
      message: null,
    };
  },
  computed: {
    ageInfo: {
      get() {
        return this.ageVal;
      },
      set(val) {
        if (this.ageValModifiers.check) {
          this.setVal(val);
        }
        this.$emit("update:ageVal", val);
        if (this.ageValModifiers.setColor) {
          this.setColor(val);
        }
      },
    },
  },

  methods: {
    setColor(val) {
      if (!val) this.$refs.inp.style.backgroundColor = "transparent";
      else if (val <= 10) this.$refs.inp.style.backgroundColor = "green";
      else if (val <= 21) this.$refs.inp.style.backgroundColor = "yellow";
      else this.$refs.inp.style.backgroundColor = "orange";
    },
    setVal(val) {
      this.message = "";
      if (val > 150) {
        this.message = "Age is incorrect should be <= 150";
      }
    },
  },
};
</script>

<style lang="css" scoped>
.message {
  color: red;
}
div {
  margin-top: 10px;
}
button {
  margin-top: 10px;
}
</style>
