<template>
  <div>
    <img :src="mask.link" alt="Image" />
    <div class="content">
      <div class="title-card">{{ mask.title }}</div>
      <div class="description">{{ mask.descrip }}</div>
      <div class="price">{{ mask.price }} руб.</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      descrip: "",
      price: "",
      link: "",
    };
  },
  setup() {},
  props: ["mask", "index"],
};
</script>
