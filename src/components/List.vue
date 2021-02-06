<template>
  <div id="list">
    <label for="newItem">Write another list item:</label>
    <input type="text" id="newItem" name="newItem" minlength="2" size="20" />
    <button>Add</button>
  </div>
</template>

<script>
export default {
  name: "List"
};
</script>

<style scoped lang="scss">
#list {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
  padding: 0.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
label,
input {
  margin: 0.5rem;
}
</style>
