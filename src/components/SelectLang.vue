<template>
  <select id="lang-select" name="lang">
    <option value="en">EN</option>
    <option value="es">ES</option>
  </select>
</template>

<script>
export default {
  name: "SelectLang"
};
</script>

<style lang="scss" scoped>
$primary-color: hsl(100deg, 50%, 50%);

#lang-select {
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
