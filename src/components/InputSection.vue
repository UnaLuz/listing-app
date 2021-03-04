<template>
  <div id="input-section">
    <label for="newItem">New list item:</label>
    <div>
      <input
        v-model="newListItem"
        type="text"
        id="newItem"
        name="newItem"
        placeholder="Make dinner..."
        minlength="2"
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
      if (this.newListItem) {
        this.$emit("add-new-item", this.newListItem);
        this.newListItem = "";
      }
    }
  }
};
</script>

<style scoped lang="scss">
$primary-color: hsl(100deg, 50%, 50%);

#input-section {
  max-width: 90%;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
}
input {
  height: 2rem;
  padding: 0.5rem;
  border: 1px solid grey;
  border-radius: 10px;
  font-family: "Montserrat", sans-serif;
  font-weight: normal;

  &:focus {
    border: 1px solid $primary-color;
  }
}
input,
button {
  margin-left: 1em;
}
label,
input,
button {
  margin-bottom: 0.5rem;
}
</style>
