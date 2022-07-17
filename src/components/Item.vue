<template>
  <div class="item">
    <img
      @click="$emit('remove', item)"
      class="item__delete"
      src="./assets/Delete.png"
      alt=""
    />
    <div class="img-block">
      <img class="img-block__image" :src="item.img" alt="No image" />
    </div>
    <h1 class="item__name">{{ item.name }}</h1>
    <div class="item__info">
      <p class="item__info-p">{{ item.info }}</p>
    </div>
    <h1 class="item__price">{{ number(item.price) }} руб.</h1>
  </div>
</template>
<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  methods: {
    number(num) {
      return num.toLocaleString("ru");
    },
  },
};
</script>
<style scoped>
.item {
  width: 332px;
  height: 423px;
  background-color: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}
.item__delete {
  position: relative;
  top: -35px;
  left: 310px;
  margin-bottom: -40px;
  opacity: 0;
}

.item:hover .item__delete {
  opacity: 1;
  transition: ease-in-out 0.5s;
}

.img-block {
  width: 332px;
  height: 200px;
}

.img-block__image {
  width: 332px;
  height: 200px;
}
.item__name {
  color: #3f3f3f;
  font-size: 20px;
  margin-left: 16px;
}
.item__info {
  width: 300px;
  height: 80px;
}
.item__info-p {
  color: #3f3f3f;
  font-size: 16px;
  margin-left: 16px;
  word-wrap: break-word;
}

.item__price {
  color: #3f3f3f;
  font-size: 24px;
  margin-top: 32px;
  margin-left: 16px;
}

.item:hover {
  cursor: pointer;
}
</style>
