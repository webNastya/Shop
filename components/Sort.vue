<template>
  <select class="currency" v-on:change="select()" v-model="selected">
    <option v-bind:value="'default'">По умолчанию</option>
    <option v-bind:value="min">По возрастанию</option>
    <option v-bind:value="max">По убыванию</option>
    <option v-bind:value="name">По наименованию</option>
  </select>
</template>
<script>
export default {
  data() {
    return {
      selected: "default",
      default: "default",
      min: "min",
      max: "max",
      name: "name",
    };
  },
  methods: {
    select() {
      let children = this.$parent.$parent.$children;
      let index = -1;
      children.forEach((el, i) => {
        if (el._name == "<Container>") {
          return (index = i);
        }
      });
      children[index].sort(this.selected);
    },
  },
};
</script>
<style lang="scss">
select {
  padding: 10px 16px;
  font-size: 12px;
  color: #b4b4b4;
  border: none;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}
</style>
