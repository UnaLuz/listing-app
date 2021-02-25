<template>
  <div id="list-item">
    <p>hello</p>
    <button>X</button>
  </div>
</template>

<script>
export default {
  name: "ListItem"
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
