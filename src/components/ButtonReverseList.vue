<template>
  <button class="iconButton" @click="$emit('change-list-order')">
    <ph-sort-descending v-if="reverseList" :size="24" weight="bold" />
    <ph-sort-ascending v-else :size="24" weight="bold" />
  </button>
</template>

<script>
import { PhSortDescending, PhSortAscending } from "phosphor-vue";

export default {
  components: {
    PhSortDescending,
    PhSortAscending
  },
  props: {
    reverseList: {
      type: Boolean,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.iconButton {
  padding: 0.3em 0.5em 0 0.5em;
  margin-bottom: 0.5em;
  margin-right: 0.5em;
}
</style>
