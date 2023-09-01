<template>
  <a-row id="globalHeader" class="grid-demo" align="center" :wrap="false">
    <a-col flex="auto">
      <a-menu
        mode="horizontal"
        :selected-keys="selectedKeys"
        @menu-item-click="doMenuClick"
      >
        <a-menu-item
          :style="{ padding: 0, marginRight: '38px', cursor: 'pointer' }"
          disabled
        >
          <div class="title-bar">
            <img src="../assets/logo.png" alt="" class="logo" />
            <div class="title">Jack OJ</div>
          </div>
        </a-menu-item>
        <a-menu-item v-for="item in visibleRoutes" :key="item.path"
          >{{ item.name }}
        </a-menu-item>
      </a-menu>
    </a-col>
    <a-col flex="100px">
      <div>{{ store.state?.user?.loginUser?.userName ?? "未登录" }}</div>
    </a-col>
  </a-row>
</template>

<script setup lang="ts">
import { routes } from "@/router/routes";
import { useRouter } from "vue-router";
import { computed, ref } from "vue";
import { useStore } from "vuex";
import checkAccess from "@/access/checkAccess";
import ACCESS_ENUM from "@/access/accessEnum";

const router = useRouter();
const store = useStore();
// 需要显示的路由
const visibleRoutes = computed(() => {
  return routes.filter((item) => {
    if (item.meta?.hidden) {
      return false;
    }
    // 根据权限过滤菜单
    if (
      !checkAccess(store.state.user?.loginUser, item?.meta?.access as string)
    ) {
      return false;
    }
    return true;
  });
});
// 默认主页
const selectedKeys = ref(["/"]);
// 路由跳转后，更新导航高亮
router.afterEach((to) => {
  selectedKeys.value = [to.path];
});

setTimeout(() => {
  store.dispatch("user/getLoginUser", {
    userName: "jack",
    userRole: ACCESS_ENUM.ADMIN,
  });
}, 3000);

// 菜单跳转
const doMenuClick = (key: string) => {
  router.push({
    path: key,
  });
};
</script>

<style scoped>
.title-bar {
  display: flex;
  align-items: center;
}

.logo {
  height: 48px;
  position: relative;
  top: 6px;
}

.title {
  margin-left: 16px;
  color: #444;
  font-weight: bold;
}
</style>
