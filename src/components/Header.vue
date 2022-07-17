<template>
  <div class="header">
    <h2 class="header__h2">Добавление товара</h2>
    <div id="v-model-select" class="">
      <select class="header__sort" v-model="selected">
        <option disabled value="">По умолчанию</option>
        <option class="header__sort">По цене min</option>
        <option>По цене max</option>
        <option>По наименованию</option>
      </select>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      selected: "",
      sortOptions: [
        { value: "title", name: "По наименованию" },
        { value: "min-max", name: "По цене min" },
        { value: "max-min", name: "По цене max" },
      ],
    };
  },
  watch: {
    selected(newValue) {
      console.log(newValue);
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
.header__sort {
  margin-right: 32px;
  margin-top: 32px;
  width: 121.49px;
  height: 36px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  user-select: none;
  overflow-x: hidden;
}
</style>
