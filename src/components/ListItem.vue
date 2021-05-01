<template>
  <li id="list-item">
    <slot></slot>
    <button @click="$emit('delete-item', itemId)" :aria-label="ariaLabel">
      X
    </button>
  </li>
</template>

<script>
export default {
  name: "ListItem",
  props: ["itemId", "ariaLabel"]
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
  }
}
</style>
