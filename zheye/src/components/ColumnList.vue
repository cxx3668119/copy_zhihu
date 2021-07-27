<template>
  <div></div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export interface ColumnProps {
  id: number;
  title: string;
  avatar: string;
  description: string;
}
export default defineComponent({
  name: "ColumnList",
  props: {
    list: {
      type: Array as PropType<ColumnProps[]>,
      required: true,
    },
  },
  setup() {
    return {};
  },
});
</script>

<style lang='less' scoped>
</style>