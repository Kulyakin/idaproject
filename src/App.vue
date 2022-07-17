<template>
  <header>
    <Header />
  </header>

  <main>
    <div class="container">
      <div>
        <LeftPanel @create="createItem" />
      </div>
      <div class="loader-block" v-if="!items.length">
        <Loader />
      </div>
      <ItemList v-bind:items="items" @remove="removeItem" />
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
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}

:root {
  font-family: "Source Sans Pro", sans-serif;
}

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
</style>
