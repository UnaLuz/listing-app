<template>
  <div id="app">
    <SelectLang @lang-change="changeLanguageTo($event)" :lang="lang" />
    <InputSection
      @add-new-item="addNewItem($event)"
      :labelTxt="staticText.InputSection.label"
      :placeholderTxt="staticText.InputSection.placeholder"
      :buttonTxt="staticText.InputSection.button"
    />
    <ul>
      <ListItem
        v-for="item in listItems"
        :key="item.id"
        :item-id="item.id"
        @delete-item="deleteListItem($event)"
      >
        {{ item.text }}
      </ListItem>
    </ul>
  </div>
</template>

<script>
import SelectLang from "./components/SelectLang.vue";
import InputSection from "./components/InputSection.vue";
import ListItem from "./components/ListItem.vue";

export default {
  name: "App",
  components: {
    SelectLang,
    InputSection,
    ListItem
  },
  data() {
    return {
      listItems: [],
      nextKey: 0,
      lang: "EN"
    };
  },
  mounted() {
    if (localStorage.getItem("itemsList")) {
      try {
        this.listItems = JSON.parse(localStorage.getItem("itemsList"));
      } catch (error) {
        console.log(
          "An error ocurred when saving 'itemsList to the local storage':\n",
          error
        );
        localStorage.removeItem("itemsList");
      }
    }
    if (localStorage.nextKey) {
      // console.log(this.nextKey, "->", localStorage.nextKey);
      this.nextKey = Number(localStorage.nextKey);
    }
    if (localStorage.lang) {
      this.lang = localStorage.lang;
    }
  },
  methods: {
    changeLanguageTo: function(selectedLang) {
      console.log("changeLanguageTo:", selectedLang);
      this.lang = selectedLang;
      this.saveLang();
    },
    addNewItem: function(itemText) {
      if (itemText) {
        this.listItems.push({
          id: this.nextKey,
          text: itemText
        });
        this.nextKey += 1;
        this.saveListData();
      }
    },
    deleteListItem: function(itemId) {
      this.listItems = this.listItems.filter(obj => {
        return obj.id !== itemId;
      });
      this.saveListData();
    },
    // Local storage
    saveLang: function() {
      localStorage.lang = this.lang;
    },
    saveListData: function() {
      const parsed = JSON.stringify(this.listItems);
      localStorage.setItem("itemsList", parsed);
      // console.log(localStorage.nextKey, "->", this.nextKey);
      localStorage.nextKey = this.nextKey;
    }
  },
  computed: {
    staticText: function() {
      switch (this.lang) {
        case "ES":
          return {
            InputSection: {
              label: "Nuevo elemento:",
              placeholder: "Hacer la cena...",
              button: "Añadir"
            }
          };

        default:
          return {
            InputSection: {
              label: "New list item:",
              placeholder: "Make dinner...",
              button: "Add"
            }
          };
      }
    }
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap");

$primary-color: hsl(100deg, 50%, 50%);
$background-color: hsl(100deg, 50%, 0%);
$active-color: hsl(100deg, 100%, 50%, 0.2);
$text-color: hsl(100deg, 0%, 85%);

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
html,
body {
  height: 100%;
}
body {
  background-color: $background-color;
}
#app {
  width: 100%;
  padding: 0.5rem;
  // Text styles
  font-family: "Montserrat", sans-serif;
  font-weight: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $text-color;
  // Flex styles
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
}

button {
  min-width: 2rem;
  min-height: 2rem;
  margin: 0%;
  padding: 0.5rem 1rem;
  border: 0.15rem solid $primary-color;
  border-radius: 10px;
  background-color: transparent;
  cursor: pointer;
  // Text related styling
  color: $primary-color;
  text-transform: uppercase;
  font-family: inherit;
  font-weight: bold;

  &:hover,
  &:focus {
    background: $primary-color;
    color: black;
  }
  &:active {
    border-color: white;
    background-color: $active-color;
    color: white;
  }
}
ul {
  width: 20rem;
  max-width: 90%;
}
</style>
