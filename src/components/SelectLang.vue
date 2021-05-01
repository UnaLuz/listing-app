<template>
  <select
    id="select-lang"
    name="lang"
    :value="selected"
    @change="$emit('lang-change', $event.target.value)"
  >
    <!--
      Can't use v-model on the select element since I don't want
      user input to directly change the value of 'selected'
    -->
    <option v-for="lang in langs" :key="lang.key" :value="lang.key">
      {{ lang.value }}
    </option>
  </select>
</template>

<script>
export default {
  name: "SelectLang",
  data() {
    return {
      default: "EN",
      langs: [
        { key: "EN", value: "English" },
        { key: "ES", value: "Español" }
      ]
    };
  },
  props: ["lang"],
  computed: {
    selected: function() {
      return this.lang || this.default;
    }
  }
};
</script>

<style lang="scss" scoped>
$primary-color: hsl(100deg, 50%, 50%);

#select-lang {
  -webkit-appearance: none;
  appearance: none;
  margin: 1rem;
  padding: 0.3rem;
  border: 1px solid grey;
  border-radius: 10px;
  background: transparent;
  cursor: pointer;
  // Flex box styles
  align-self: flex-end;
  // Text styles
  font-family: inherit;
  font-weight: bold;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $primary-color;

  &:hover,
  &:focus {
    background: $primary-color;
    color: black;
  }
}
</style>
