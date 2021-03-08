<template>
  <li id="list-item">
    <slot></slot>
    <button @click="$emit('delete-item', itemId)">X</button>
  </li>
</template>

<script>
export default {
  name: "ListItem",
  props: ["itemId"]
};
</script>

<style scoped lang="scss">
$primary-color: hsla(100deg, 75%, 50%, 0.25);

#list-item {
  padding: 8px;
  border-top: 2px solid $primary-color;
  // Flex styles
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
  flex-grow: 1;

  button {
    flex-grow: 0;
    flex-shrink: 0;
  }
}
</style>
