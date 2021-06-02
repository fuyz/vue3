<template>
  <h1>{{ msg }}</h1>
  <button @click="count++">count is: {{ count }}</button>
  <p>{{ number }}</p>
  <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
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
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup () {

    const number = ref<number>(100)
    // setInterval(() => {
    //   number.value++
    // }, 1000)

    watchEffect(() => {
      console.log(number.value)
    })

    const state = reactive({
      count: 1
    })

    return {
      // count,
      ...toRefs(state),
      number
    }
  }
})
</script>
