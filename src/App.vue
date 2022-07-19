<template>
  <header class="header-up">
    <Header />
    <div id="v-model-select" class="">
      <select class="header__sort" v-model="selected">
        <option disabled value="">По умолчанию</option>
        <option value="min-max" class="header__sort">По цене min</option>
        <option value="max-min">По цене max</option>
        <option value="name">По наименованию</option>
      </select>
    </div>
  </header>

  <main>
    <div class="container">
      <div>
        <LeftPanel @create="createItem" />
      </div>
      <div class="loader-block" v-if="!items.length">
        <Loader />
      </div>
      <ItemList v-bind:items="sortedItems" @remove="removeItem" />
    </div>
  </main>
</template>

<script>
import LeftPanel from "./components/LeftPanel.vue";
import Header from "./components/Header.vue";
import Loader from "./components/Loader.vue";
import ItemList from "./components/ItemList.vue";
export default {
  components: { LeftPanel, Header, Loader, ItemList },
  data() {
    return {
      items: [],
      selected: "",
      sortOptions: [
        { value: "name", name: "По наименованию" },
        { value: "min-max", name: "По цене min" },
        { value: "max-min", name: "По цене max" },
      ],
    };
  },
  mounted() {
    if (localStorage.getItem("items")) {
      try {
        this.items = JSON.parse(localStorage.getItem("items"));
      } catch (e) {
        localStorage.removeItem("items");
      }
    }
  },
  methods: {
    createItem(item) {
      this.items.push(item);
      localStorage.setItem("items", JSON.stringify(this.items));
    },
    removeItem(item) {
      this.items = this.items.filter((i) => i.id !== item.id);
      localStorage.setItem("items", JSON.stringify(this.items));
    },
  },
  computed: {
    sortedItems() {
      console.log(this.selected);
      if (this.selected == "name") {
        return [...this.items].sort((item1, item2) => {
          return item1[this.selected]?.localeCompare(item2[this.selected]);
        });
      }
      if (this.selected == "min-max") {
        return [...this.items].sort(
          (item1, item2) => item1.price - item2.price
        );
      }
      if (this.selected == "max-min") {
        console.log(this.selected);
        return [...this.items].sort(
          (item1, item2) => item2.price - item1.price
        );
      } else return this.items;
    },
  },
};
</script>

<style sxoped>

.container {
  max-width: 1440px;
  height: 900px;
  display: flex;
}

@media screen and (max-width: 600px) {
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}

.loader-block {
  margin: 30vh auto;
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

.header-up {
  max-width: 1440px;
  height: 83px;
  justify-content: space-between;
  display: flex;
}
</style>
