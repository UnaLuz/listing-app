<template>
  <div id="input-section">
    <label for="newItem">{{ labelTxt }}</label>
    <div>
      <input
        v-model="newListItem"
        type="text"
        id="newItem"
        name="newItem"
        :placeholder="placeholderTxt"
        minlength="2"
        @keyup.enter="addItem()"
      />
      <button @click="addItem()">{{ buttonTxt }}</button>
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
  props: {
    labelTxt: {
      type: String,
      required: false,
      default: "New list item:"
    },
    placeholderTxt: {
      type: String,
      required: false,
      default: "Make dinner..."
    },
    buttonTxt: {
      type: String,
      required: false,
      default: "Add"
    }
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
  // Flex styles
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  margin-bottom: 0.5em;
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
</style>
