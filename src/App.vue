<template>
  <div id="app">
    <List
      :list-items="listItems"
      @delete-list-item="deleteListItem($event)"
      @add-item="addNewItem($event)"
    />
  </div>
</template>

<script>
import List from "./components/List.vue";

export default {
  name: "App",
  components: {
    List
  },
  data() {
    return {
      listItems: [
        {
          id: 1,
          text: "Do the dishes"
        },
        {
          id: 2,
          text: "Mow the lawn"
        }
      ]
    };
  },
  methods: {
    deleteListItem: function(itemId) {
      this.listItems = this.listItems.filter(obj => {
        return obj.id !== itemId;
      });
    },
    addNewItem: function(itemText) {
      if (itemText) {
        this.listItems.push({
          id: this.listItems.length + 1,
          text: itemText
        });
      }
    }
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}
body {
  background-color: hsl(100deg, 10%, 5%);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: hsl(100deg, 0%, 75%);
  margin-top: 6vh;
  display: flex;
  justify-content: center;
}
</style>
