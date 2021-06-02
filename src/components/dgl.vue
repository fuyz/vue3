<template>
  <el-dialog title="提示" v-model="isShowDgl" width="800px" center @close="closeDgl">
    <div>
      <h2>弹框组件</h2>
      <h3>{{ title }}</h3>
      <el-row :gutter="10">
        <el-col :span="6">
          <el-button type="primary" @click="add">{{ count }}</el-button>
        </el-col>
        <el-col :span="6">
          <span>count的平方：{{ countPf }}</span>
        </el-col>
        <el-col :span="6">
          <el-button type="primary" @click="minus">{{ number }}</el-button>
          <p>number.value:{{ number.value }}</p>
        </el-col>
      </el-row>

      <el-collapse>
        <el-collapse-item title="defineComponent" name="1">
          <div>在使用组件的地方组件通过export default defineComponent({options}) 的写法暴露出去，而不是Vue2的export default写法，以上报错组件的代码改为即可消除警告并实现功能。</div>
        </el-collapse-item>
      </el-collapse>

      <el-row :gutter="10">
        <el-col :span="6">
          <el-button type="primary" @click="confirm">emit fn</el-button>
        </el-col>
      </el-row>

    </div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="isShowDgl = false">取 消</el-button>
        <el-button type="primary" @click="isShowDgl = false">确 定</el-button>
      </span>
    </template>
  </el-dialog>
</template>
<script lang="ts">
import {
  reactive,
  toRefs,
  computed,
  onMounted,
  onUnmounted,
  ref,
  watch,
  watchEffect,
  defineComponent,
} from "vue";
export default defineComponent({
  name: "Dgl",
  props: {
    title: String,
    visible: Boolean
  },
  emits: ['confirm', 'update:visible'],
  setup (props, context) {
    console.log('setup')
    console.log([props, context]);
    const number = ref<number>(100)
    // setInterval(() => {
    //   number.value++
    // }, 1000)

    watchEffect(() => {
      console.log(number)
    })
    const cupsArr = ref([])
    console.log(cupsArr, cupsArr.value)
    const state = reactive({
      isShowDgl: false,
      name: "fuyz",
      count: 0,
      countPf: 0,
    });
    const methods = {
      add: () => {
        state.count++;
        cupsArr.value.push('a')
        console.log(state)watch
      },
      minus () {
        number.value += 20
      },
      confirm: () => {
        context.emit("confirm", "i am from dgl component");
      },
      closeDgl () {
        context.emit('update:visible', false)
      }
    };
    watch(
      () => state.count,
      (val, oldVal) => {
        state.countPf = val * val;
      },
      {
        immediate: true,
        deep: true,
      }
    );
    watch(
      () => props.visible,
      (val, oldVal) => {
        state.isShowDgl = val
      },
      {
        immediate: true,
      }
    );
    //页面加载完成
    onMounted(() => {
      console.log('onMounted')
    });
    //销毁
    onUnmounted(() => {
      console.log('unonMounted')
    });

    return {
      ...toRefs(state),
      // ...state,
      ...methods,
      number,
      cupsArr
    };
  },

  beforeCreate () {
    console.log('----beforeCreate----')
  },
  created () {
    console.log('----created----')
  }
});
</script>
