<template>
  <li id="list-item">
    <slot></slot>
    <button @click="$emit('delete-item', itemId)" :aria-label="ariaLabel">
      <ph-x :size="20" weight="bold" />
    </button>
  </li>
</template>

<script>
import { PhX } from "phosphor-vue";
export default {
  components: {
    PhX
  },
  props: {
    itemId: {
      type: Number,
      required: true
    },
    ariaLabel: String
  }
};
</script>

<style scoped lang="scss">
$item-border: hsla(100deg, 50%, 50%, 0.35);

#list-item {
  padding: 0.5rem;
  border-top: 2px solid $item-border;
  text-align: justify;
  // Flex styles
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;

  button {
    margin-left: 0.5rem;
    flex-grow: 0;
    flex-shrink: 0;
    padding: 0.2em 0.5em 0 0.5em;
  }
}
</style>
