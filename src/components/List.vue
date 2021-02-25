<template>
  <div id="list-component">
    <section>
      <InputSection />
    </section>
    <section>
      <ListItem />
    </section>
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
  }
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
