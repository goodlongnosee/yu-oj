<template>
  <div id="basicLayout">
    <a-layout style="min-height: 100vh">
      <a-layout-header class="header">
        <global-header />
      </a-layout-header>
      <a-layout-content class="content">
        <router-view />
      </a-layout-content>
      <a-layout-footer class="footer"
        ><a href="https://github.com/goodlongnosee" target="_blank"
          >my-oj-system</a
        ></a-layout-footer
      >
    </a-layout>
  </div>
</template>

<script>
import GlobalHeader from "@/components/GlobalHeader.vue";

export default {
  name: "BasicLayout",
  components: { GlobalHeader },
};
</script>

<style scoped>
#basicLayout .header {
  margin-bottom: 6px;
  box-shadow: #eee 1px 1px 5px;
}

#basicLayout .content {
  background: linear-gradient(to right, #bbb, #fff);
  margin-bottom: 16px;
  padding: 20px;
}

#basicLayout .footer {
  background-color: #efefef;
  padding: 16px;
  position: static;
  left: 0;
  bottom: 0;
  right: 0;
  text-align: center;
}
</style>
