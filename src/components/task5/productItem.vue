<template>
  <div class="container-item">
    <a :href="itemData.link" target="_blank">
      <div class="container-image">
        <img :src="itemData.imgSrc" alt="Картинки нет" />
      </div>
      <h4 class="item-title">{{ itemData.title }}</h4>
      <div class="item-price">{{ itemData.price }}₴</div>
    </a>
  </div>
</template>

<script>
export default {
  name: "productItem",
  props: {
    itemData: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>

<style lang="scss" scoped>
.container-item {
  border: 1px solid white;
  border-radius: 10%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 10px;
  transition: border 0.3s ease 0s;
  &:hover {
    border: 1px solid black;
    transition: border 0.3s ease 0s;
  }
  a {
    color: black;
    text-decoration: none;
  }
}
.container-image {
  img {
    width: 250px;
  }
}
.item-price {
  font-size: 24px;
  color: red;
}
</style>
