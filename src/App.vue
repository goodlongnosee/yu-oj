<template>
  <div id="app">
    <BasicLayout />
  </div>
</template>

<style>
#app {
}
</style>
<script setup lang="ts">
import BasicLayout from "@/layouts/BasicLayout";
import { onMounted } from "vue";
// import { useRouter } from "vue-router";
// import { useStore } from "vuex";

/**
 * 全局初始化函数，放置全局单次调用的函数
 */
const doInit = () => {
  console.log("12312123");
};

onMounted(() => {
  doInit();
});
// const store = useStore();
// const router = useRouter();
// router.beforeEach((to, from, next) => {
//
//   next();
// });
</script>
