<template>
  <div id="input-section">
    <label for="newItem">{{ label }}</label>
    <div>
      <input
        v-model="newListItem"
        type="text"
        id="newItem"
        name="newItem"
        :placeholder="placeholder"
        minlength="2"
        @keyup.enter="addItem()"
      />
      <button @click="addItem()">{{ addButtonTxt }}</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newListItem: ""
    };
  },
  props: ["labelTxt", "placeholderTxt", "buttonTxt"],
  methods: {
    addItem: function() {
      if (this.newListItem) {
        this.$emit("add-new-item", this.newListItem);
        this.newListItem = "";
      }
    }
  },
  computed: {
    // In case there was a problem with the props passed:
    label: function() {
      return this.labelTxt || "New list item:";
    },
    placeholder: function() {
      return this.placeholderTxt || "Make dinner...";
    },
    addButtonTxt: function() {
      return this.buttonTxt || "Add";
    }
  }
};
</script>

<style scoped lang="scss">
$primary-color: hsl(100deg, 50%, 50%);

#input-section {
  max-width: 90%;
  // Flex styles
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
  // Text styles
  font-family: inherit;
  font-weight: normal;
  font-size: 0.85rem;

  &:focus {
    border-color: $primary-color;
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
