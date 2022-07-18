<template>
  <div class="header">
    <h2 class="header__h2">Добавление товара</h2>
  </div>
</template>
<script>
export default {
  data() {
    return {
      selected: "",
      sortOptions: [
        { value: "name", name: "По наименованию" },
        { value: "min-max", name: "По цене min" },
        { value: "max-min", name: "По цене max" },
      ],
    };
  },

  watch: {
    selected(newValue) {
      this.posts.sort((item1, item2) => {
        return item1[newValue]?.localeCompare(item2[newValue]);
      });
    },
  },
};
</script>

<style>
.header {
  max-width: 1440px;
  max-height: 83px;
  background-color: rgba(255, 254, 251, 0.8);
  display: flex;
  justify-content: space-between;
}

@media screen and (max-width: 400px) {
  .header {
    max-height: 100px;
  }
}

.header__h2 {
  margin-left: 32px;
  margin-top: 32px;
}
</style>
