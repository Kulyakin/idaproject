<template>
  <div class="wrap" v-if="items.length">
    <transition-group name="item-list">
      <Item
        v-for="item in items"
        :item="item"
        :key="item.id"
        @remove="$emit('remove', item)"
      />
    </transition-group>
  </div>
</template>
<script>
import Item from "./Item.vue";
export default {
  props: {
    items: {
      type: Array,
      requared: true,
    },
  },
  components: { Item },
};
</script>

<style scoped>
.wrap {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 16px;
}

.item-list-enter-active,
.item-list-leave-active {
  transition: all 1s ease;
}
.item-list-enter-from,
.item-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.item-list-move {
  transition: transform 0.8s ease;
}
</style>
