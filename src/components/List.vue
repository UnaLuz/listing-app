<template>
  <div id="list-component">
    <InputSection @add-new-item="$emit('add-item', $event)" />
    <ul>
      <li
        is="list-item"
        v-for="item in listItems"
        :key="item.id"
        :item-text="item.text"
        :item-id="item.id"
        @delete-item="$emit('delete-list-item', $event)"
      ></li>
    </ul>
  </div>
</template>

<script>
import InputSection from "./InputSection.vue";
import ListItem from "./ListItem.vue";
export default {
  name: "ListComponent",
  components: {
    InputSection,
    ListItem
  },
  props: ["listItems"]
};
</script>

<style scoped lang="scss">
#list-component {
  padding: 0.5rem;
  margin-top: 0px;
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  align-items: center;
}
</style>
