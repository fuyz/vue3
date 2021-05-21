<template>
  <el-dialog title="提示" v-model="visible" width="30%" center>
    <div>
      <h2>弹框组件</h2>
      <h3>{{ title }}</h3>
      <div>
        <el-button type="primary" @click="add">{{ count }}</el-button>
        <span>count的平方：{{ countPf }}</span>
      </div>
      <el-button type="primary" @confirm="confirm"></el-button>
      <el-collapse>
        <el-collapse-item title="dedineComponent" name="1">
          <div>在使用组件的地方组件通过export default dedineComponent({options}) 的写法暴露出去，而不是Vue2的export default写法，以上报错组件的代码改为即可消除警告并实现功能。</div>
        </el-collapse-item>
      </el-collapse>
    </div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="visible = false">取 消</el-button>
        <el-button type="primary" @click="visible = false">确 定</el-button>
      </span>
    </template>
  </el-dialog>
</template>
<script>
import {
  reactive,
  toRefs,
  computed,
  onMounted,
  onUnmounted,
  ref,
  watch,
  dedineComponent,
} from "vue";
export default dedineComponent({
  name: "Dgl",
  setup(props, context) {
    console.log([props, context]);

    const state = reactive({
      visible: false,
      name: "fuyz",
      count: 0,
      countPf: 0,
    });
    const methods = {
      add: () => {
        state.count++;
      },
      confirm: () => {
        context.$emit("confirm", "i am from dgl component");
      },
    };
    watch(
      count,
      (val, oldVal) => {
        state.countPf = val * val;
      },
      {
        immediate: true,
        deep: true,
      }
    );
    //页面加载完成
    onMounted(() => {});
    //销毁
    onUnmounted(() => {});

    return {
      ...toRefs(state),
      ...methods,
    };
  },
});
</script>
