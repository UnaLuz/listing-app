<template>
  <div id="app">
    <SelectLang
      @lang-change="changeLanguageTo($event)"
      :lang="lang"
      :ariaLabel="staticText.SelectLang.ariaLabel"
    />
    <InputSection
      @add-new-item="addNewItem($event)"
      :labelTxt="staticText.InputSection.label"
      :placeholderTxt="staticText.InputSection.placeholder"
      :buttonTxt="staticText.InputSection.button"
    />
    <ul class="buttonList">
      <ButtonReverseList
        :reverseList="reverseList"
        @change-list-order="changeListOrder()"
      />
    </ul>
    <ul class="itemList" :class="{ reverse: reverseList }">
      <ListItem
        v-for="item in listItems"
        :key="item.id"
        :item-id="item.id"
        :ariaLabel="staticText.ListItem.ariaLabel"
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
import ButtonReverseList from "./components/ButtonReverseList.vue";

export default {
  name: "App",
  components: {
    SelectLang,
    InputSection,
    ListItem,
    ButtonReverseList
  },
  data() {
    return {
      listItems: [],
      nextKey: 0,
      lang: "EN",
      reverseList: false
    };
  },
  mounted() {
    // Check if there are list items in the local storage when mounted
    if (localStorage.getItem("itemsList")) {
      try {
        this.listItems = JSON.parse(localStorage.getItem("itemsList"));
      } catch (error) {
        console.log(
          "An error ocurred when retrieving 'itemsList' from the local storage:\n",
          error
        );
        localStorage.removeItem("itemsList"); // Assume the item is corrupted and delete it
      }
    }
    if (localStorage.nextKey) {
      this.nextKey = Number(localStorage.nextKey);
    }
    if (localStorage.lang) {
      this.lang = localStorage.lang;
    }
  },
  methods: {
    changeLanguageTo: function(selectedLang) {
      const validLangs = ["EN", "ES"];

      // Make sure that the selected language is valid
      if (validLangs.indexOf(selectedLang) !== -1) {
        this.lang = selectedLang;
        this.saveLang();
      }
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
      try {
        localStorage.setItem("itemsList", parsed); // Save list items to the local storage
        localStorage.nextKey = this.nextKey; // Save the next key to not have duplicates
      } catch (err) {
        console.log(
          "An error ocurred saving 'itemsList' to the local storage:",
          err
        );
        localStorage.removeItem("itemsList"); // Assume the item is corrupted and delete it
      }
    },
    changeListOrder: function() {
      // Change sorting directionof the list
      this.reverseList = !this.reverseList;
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
            },
            SelectLang: {
              ariaLabel: "Seleccione un lenguaje"
            },
            ListItem: {
              ariaLabel: "Eliminar"
            }
          };

        default:
          return {
            InputSection: {
              label: "New list item:",
              placeholder: "Make dinner...",
              button: "Add"
            },
            SelectLang: {
              ariaLabel: "Select a language"
            },
            ListItem: {
              ariaLabel: "Delete"
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
.buttonList {
  display: flex;
  flex-direction: row;
}
.itemList {
  display: flex;
  flex-direction: column;
}
.reverse {
  flex-direction: column-reverse;
}
</style>
