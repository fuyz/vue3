<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3.0 + Vite" />
  <el-button type="primary" @click="isShowDgl = true">show dgl</el-button>
  <!-- '.sync' modifier on 'v-bind' directive is deprecated. Use 'v-model:propName' instead. -->
  <!-- <Dgl :visible.sync="isShowDgl" :title="title"></Dgl> -->
  <Dgl v-model:visible="isShowDgl" :title="title" @confirm="confirmFn"></Dgl>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Dgl: () => import("./components/dgl.vue"),
  },
  data() {
    return {
      isShowDgl: false,
      title: "i am a title from app.vue",
    };
  },
  methods: {
    confirmFn(params) {
      this.$message.success(params);
    },
  },
};
</script>
