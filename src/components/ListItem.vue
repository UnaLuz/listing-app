<template>
  <li id="list-item">
    {{ itemText }}
    <button @click="$emit('delete-item', itemId)">X</button>
  </li>
</template>

<script>
export default {
  name: "ListItem",
  props: ["itemText", "itemId"]
};
</script>

<style scoped lang="scss">
#list-item {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
}
p,
button {
  margin: 0.5rem;
}
</style>
