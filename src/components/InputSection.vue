<template>
  <div id="input-section">
    <label for="newItem">Write another list item:</label>
    <div>
      <input
        v-model="newListItem"
        type="text"
        id="newItem"
        name="newItem"
        minlength="2"
        size="20"
      />
      <button @click="addItem()">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "InputSection",
  data() {
    return {
      newListItem: ""
    };
  },
  methods: {
    addItem: function() {
      if (this.newListItem && this.newListItem.length > 1) {
        this.$emit("add-new-item", this.newListItem);
        this.newListItem = "";
      }
    }
  }
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
