<template>
  <div id="input-section">
    <label for="newItem">Write another list item:</label>
    <div>
      <input type="text" id="newItem" name="newItem" minlength="2" size="20" />
      <button>Add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "InputSection"
};
</script>

<style scoped lang="scss">
#input-section {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
}
label,
input {
  margin: 0.5rem;
}
</style>
