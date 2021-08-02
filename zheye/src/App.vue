<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <column-list :list="list"> </column-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";
import ColumnList, { ColumnProps } from "./components/ColumnList.vue";
import GlobalHeader, { UserProps } from "./components/GlobalHeader.vue";

const currentUser: UserProps = {
  isLogin: true,
  name: "cxx",
  id: 1,
  // isLogin: false,
};
const testData: ColumnProps[] = [
  {
    id: 1,
    title: "cxx1",
    description: "cxx的练习demo",
    avatar:
      "http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100",
  },
  {
    id: 2,
    title: "cxx2",
    description: "cxx的练习demo",
  },
  {
    id: 3,
    title: "cxx3",
    description: "cxx的练习demo",
    avatar:
      "http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100",
  },
  {
    id: 4,
    title: "cxx4",
    description: "cxx的练习demo",
    avatar:
      "http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100",
  },
];
export default defineComponent({
  name: "App",
  components: {
    ColumnList,
    GlobalHeader,
  },
  setup() {
    return {
      list: testData,
      currentUser: currentUser,
    };
  },
});
</script>

<style lang="less">
</style>
