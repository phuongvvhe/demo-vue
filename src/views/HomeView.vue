<script lang="ts">
import { defineComponent } from 'vue';
import AboutView from './AboutView.vue';
import AddView from './AddView.vue'

export default defineComponent({
  components: {
    // SmileOutlined,
    // DownOutlined,
    AddView,
    AboutView
  },
  // setup() {
  //   return {
  //     data,
  //     columns,
  //   };
  // },
});

</script>

<template>
  <a-layout>
    <a-layout-header class="header">
      <div class="logo" />
      <a-menu
          v-model:selectedKeys="selectedKeys1"
          theme="dark"
          mode="horizontal"
          :style="{ lineHeight: '64px' }"
      >
        <a-menu-item key="1">nav 1</a-menu-item>
        <a-menu-item key="2">nav 2</a-menu-item>
        <a-menu-item key="3">nav 3</a-menu-item>
      </a-menu>
    </a-layout-header>
    <a-layout>
      <AboutView></AboutView>

    </a-layout>
    <a-layout>
      <AddView></AddView>

    </a-layout>
  </a-layout>
</template>
<style>
#components-layout-demo-top-side-2 .logo {
  float: left;
  width: 120px;
  height: 31px;
  margin: 16px 24px 16px 0;
  background: rgba(255, 255, 255, 0.3);
}

.ant-row-rtl #components-layout-demo-top-side-2 .logo {
  float: right;
  margin: 16px 0 16px 24px;
}

.site-layout-background {
  background: #fff;
}
</style>