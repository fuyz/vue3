# vue3

基于Vue3+vite框架，采用GitHub Action 实现自动构建、部署

 <img src="https://user-images.githubusercontent.com/21302802/118791950-c4863880-b8c9-11eb-9f33-676479e94249.png" alt="log" style="width:100px;" width="200px">

### Vue2 VS Vue3
<details >
  <summary><b>生命周期</b></summary>
  <ul>
   <li>
     <img src="https://user-images.githubusercontent.com/21302802/119072886-ddecc900-ba1e-11eb-94c9-2ad1778242a1.png" alt="Vue2 VS Vue3" style="max-width:100%;">
   </li>
  </ul>
</details>

<details open>
  <summary><b>语法差异总结：</b></summary>
  <ol>
    <li>
      <b>组件封装：.sync标识</b>
      <pre>
        ❌ &lt;Dgl :visible.sync="isShowDgl" :title="title"&gt; &lt;/Dgl&gt;
        error: '.sync' modifier on 'v-bind' directive is deprecated. Use 'v-model:propName' instead.
        ✅ &lt;Dgl v-model:visible="isShowDgl" :title="title" @confirm="confirmFn"&gt;&lt;/Dgl&gt;
      </pre>
    </li>
    <li>
      <b>组件定义</b>
      <pre>
        v2: export default {}
        v3: export default defineComponent({})
      </pre>
      <p>
        在 Vue 3 的 Composition API 中，采用了 setup() 作为组件的入口函数。
        在结合了 TypeScript 的情况下，传统的 Vue.extend 等定义方法无法对此类组件给出正确的参数类型推断，这就需要引入 defineComponent() 组件包装函数，其在 rfc 文档中的说明为：<a href="https://composition-api.vuejs.org/api.html#setup">文档说明</a>
      </p>
    </li>
    <li>
      <b>组件封装：emit方法使用前需要先注册</b>
      <img src="https://user-images.githubusercontent.com/21302802/119456340-2b459f00-bd6d-11eb-8808-3ac727999e61.png" width="100%" />
    </li>
    <li>
      <b>组件封装：导入动态组件</b>
      <pre>
      import { defineAsyncComponent } from 'vue'
      components: {
        RoleConfig: defineAsyncComponent(() => import('./roleConfig.vue'))
      },
      </pre>
    </li>
    <li>
      <b>html元素ref对象</b>
      <pre>
        html:
        &lt;el-form ref="formRef" :model="formData" inline label-width="0px" size="small">&lt;/el-form>
        js: 定义和调用
        const formRef: Ref = ref(null)
        formRef.value.resetFields()
      </pre>
    </li>
    <li>
      <b>动态定义的ref: getCurrentInstance</b>
      <pre>
        html:
        &lt;TabTable v-if="activeTab === item.platform" :ref="item.platform+'Ref'" :permissionTreeData="item.permissionTreeData" :platformType="item.platform" :disabled="false">&lt;/TabTable>
        js:
        import { getCurrentInstance } from 'vue'
        const currentInstance: any = getCurrentInstance()
        fn (oldPlatformType) {
          currentInstance.refs[oldPlatformType + 'Ref'].getCurrentCheckedData()
        }
      </pre>
    </li>
    <li>
      <b>html元素ref对象</b>
      <pre>
        html:
        &lt;el-form ref="formRef" :model="formData" inline label-width="0px" size="small">&lt;/el-form>
        js: 定义和调用
        const formRef: Ref = ref(null)
        formRef.value.resetFields()
      </pre>
    </li>
    <li>
      <b>路由：<a href="https://next.router.vuejs.org/zh/guide/advanced/composition-api.html#%E5%9C%A8-setup-%E4%B8%AD%E8%AE%BF%E9%97%AE%E8%B7%AF%E7%94%B1%E5%92%8C%E5%BD%93%E5%89%8D%E8%B7%AF%E7%94%B1">官方文档</a></b>
      <pre>
        import { useRoute, useRouter } from 'vue-router'
        const route = useRoute()
        const router = useRouter()
        router.push(path)
        route.query.roleId
      </pre>
    </li>
    <li>
      <b>导航守卫</b>
      <pre>
        import { onBeforeRouteLeave, onBeforeRouteUpdate } from 'vue-router'
        // 与 beforeRouteLeave 相同，无法访问 `this`
        onBeforeRouteLeave((to, from) => {
          const answer = window.confirm(
            'Do you really want to leave? you have unsaved changes!'
          )
          // 取消导航并停留在同一页面上
          if (!answer) return false
        })
        const userData = ref()
        // 与 beforeRouteLeave 相同，无法访问 `this`
        onBeforeRouteUpdate(async (to, from) => {
          //仅当 id 更改时才获取用户，例如仅 query 或 hash 值已更改
          if (to.params.id !== from.params.id) {
            userData.value = await fetchUser(to.params.id)
          }
        })
      </pre>
    </li>
 </ol>
</details>

### 启动、部署

<details >
  <summary><b>how to start</b></summary>

```
 #创建项目
 npm init vite-app <project-name>
 cd <project-name>
 npm install
 npm run dev

 #本地启动
 npm run dev

 #打包
 npm run build

```
</details>

<details>
  <summary><b>GitHub pages站点</b></summary>

- [使用 Jekyll 创建 GitHub Pages 站点](https://docs.github.com/cn/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

</details>
<details>
  <summary><b>github Action</b></summary>

- [GitHub Actions 入门教程](https://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)

- [什么是 GitHub Action 么？React项目实配](https://www.cnblogs.com/babycomeon/p/12771624.html)

- 官方服务：https://github.com/actions

 </detail>
