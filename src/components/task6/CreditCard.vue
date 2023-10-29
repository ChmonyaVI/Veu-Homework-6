<template>
  <div class="container-class">
    <label class="card">СARD NUMBER <input maxlength="19" type="text" v-model="cardValue" /></label>
    <div class="second-row">
      <label>EXPIRY DATE <input maxlength="5" type="text" v-model="valDate" /></label>
      <label>SECURE CODE <input maxlength="3" type="text" v-model="valSecure" /></label>
    </div>
  </div>
</template>

<script>
export default {
  name: "CreditCard",
  props: {
    cardNumber: { type: String },
    cardNumberModifiers: { default: () => ({}) },
    expVal: {
      type: String,
    },
    secureModifiers: () => ({}),
    secureVal: {
      type: String,
    },
    valModifiers: () => ({}),
  },

  computed: {
    cardValue: {
      get() {
        return (this.cardNumber ?? "").toString().replace(/(\d{4}(?=\S+))/g, "$1 ");
      },
      set(val) {
        val = val.replace(/\D/g, "");

        this.$emit("update:cardNumber", val);
      },
    },
    valDate: {
      get() {
        return (this.expVal ?? "").toString().replace(/^\d+\/\d+$/);
      },
      set(val) {
        this.$emit("update:expVal", val);
      },
    },
  },
};
</script>

<style lang="scss" scoped></style>
