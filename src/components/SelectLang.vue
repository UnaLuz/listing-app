<template>
  <select
    id="select-lang"
    name="lang"
    v-model="selected"
    @change="$emit('lang-change', selected)"
  >
    <option v-for="lang in langs" :key="lang.key" :value="lang.value">
      {{ lang.value }}
    </option>
  </select>
</template>

<script>
export default {
  name: "SelectLang",
  data() {
    return {
      selected: "EN",
      langs: [
        { key: 0, value: "EN" },
        { key: 1, value: "ES" }
      ]
    };
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
  // Flex box styles
  align-self: flex-end;
  // Text styles
  font-family: inherit;
  font-weight: bold;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $primary-color;
}
</style>
