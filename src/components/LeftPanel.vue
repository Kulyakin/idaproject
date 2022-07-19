<template>
  <form @submit.prevent class="left-panel">
    <div class="label-wrap">
      <label id="name" class="name">Наименование товара</label>
      <input
        v-model="item.name"
        id="name"
        class="left-panel__input"
        type="text"
        placeholder="Введите наименование товара"
      />
    </div>
    <div class="label-wrap">
      <label class="name">Описание товара</label>
      <textarea
        v-model="item.info"
        class="left-panel__info-input"
        type="text"
        placeholder="Введите описание товара"
      ></textarea>
    </div>
    <div class="label-wrap">
      <label class="name">Ссылка на изображение товара</label>
      <input
        v-model="item.img"
        class="left-panel__input"
        type="text"
        placeholder="Введите ссылку"
      />
    </div>
    <div class="label-wrap">
      <label class="name">Цена товара</label>
      <input
        v-model="item.price"
        class="left-panel__input"
        type="number"
        placeholder="Введите цену"
      />
    </div>
    <button @click="createItem" class="btn">Добавить товар</button>
  </form>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, minLength } from "@vuelidate/validators";

export default {
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      item: {
        name: "",
        info: "",
        img: "",
        price: "",
      },
    };
  },
  validations() {
    return {
      item: {
        name: { required, minLength: minLength(3) },
        img: { required, minLength: minLength(3) },
        price: { required },
      },
    };
  },
  computed: {
    nameErrors() {
      const errors = [];
      if (this.$v.$silentErrors) return errors;
    },
  },
  methods: {
    createItem() {
      this.item.id = Date.now();
      this.item.key = this.item.id;
      this.$emit("create", this.item);
      this.item = {
        name: "",
        info: "",
        img: "",
        price: "",
      };
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./assets/variables.scss";
.name {
  position: relative;
  font-size: 10px;
  margin-bottom: 4px;
}

.label-wrap {
  display: flex;
  flex-direction: column;
}
.left-panel {
  width: 332px;
  height: 440px;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-right: 16px;
  margin-bottom: 16px;
}

.left-panel__input {
  width: 268px;
  height: 36px;
  padding: 0 0 0 16px;
  color: $placeholder-color;

  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
}

.left-panel__input:required {
  border: 1px solid red;
}

.left-panel__input:enabled {
  border: 1px solid white;
}

.left-panel__info-input {
  width: 268px;
  height: 108px;
  padding: 10px 0 0 16px;
  color: $placeholder-color;
  resize: none;
  font-family: "Source Sans Pro", sans-serif;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: none;
  font-size: 14px;
}

.btn {
  width: 284px;
  height: 36px;
  left: 56px;
  top: 463px;
  padding: 0;

  background: #eeeeee;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}

.btn:hover {
  opacity: 0.7;
}
</style>
