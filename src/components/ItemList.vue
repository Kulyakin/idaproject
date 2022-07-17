<template>
  <div class="wrap" v-if="items.length">
    <transition-group name="list">
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

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
