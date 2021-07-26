<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{ count }}</h1>
    <h1>{{ double }}</h1>
    <ul>
      <li v-for="number in numbers" :key="number">
        <h1>{{ number }}</h1>
      </li>
    </ul>
    <h1 v-if="loading">Loading...</h1>
    <img v-if="loaded" :src="result.message" alt="" />
    <h1>{{ person.name }}</h1>
    <button @click="increase">👍+1</button>
  </div>
</template>

<script lang="ts">
import { computed, reactive, toRefs, onMounted, onUpdated, watch } from "vue";
import useURLLoader from "./hooks/useURLLoaders";
// 解决
interface DataProps {
  count: number;
  double: number;
  increase: () => void;
  numbers: number[];
  person: { name?: string };
}

interface DogResult {
  message: string;
  status: string;
}

export default {
  name: "App",
  components: {},
  setup() {
    // const count = ref(0);
    // const double = computed(() => {
    //   return count.value * 2;
    // });
    // const increase = () => {
    //   count.value++;
    // };

    // onMounted
    onMounted(() => {
      console.log("mounted");
    });
    onUpdated(() => {
      console.log("updated");
    });
    // onRenderTracked((e) => {
    //   console.log(e);
    // });
    const data: DataProps = reactive({
      // 类型推断错误
      count: 0,
      increase: () => {
        data.count++;
      },
      double: computed(() => data.count * 2),
      numbers: [0, 1, 2],
      person: {},
    });

    const { result, loading, loaded } = useURLLoader<DogResult>(
      "https://dog.ceo/api/breeds/image/random"
    );
    watch(result, () => {
      if (result.value) {
        console.log("value", result.value.message);
      }
    });
    data.numbers[0] = 5;
    data.person.name = "cxx";
    const refData = toRefs(data);
    return {
      ...refData,
      loading,
      loaded,
      result,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
