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
     v3: export default defineComponent({})</pre>
     <p>
      在 Vue 3 的 Composition API 中，采用了 setup() 作为组件的入口函数。
      在结合了 TypeScript 的情况下，传统的 Vue.extend 等定义方法无法对此类组件给出正确的参数类型推断，这就需要引入 defineComponent() 组件包装函数，其在 rfc 文档中的说明为：<a href="https://composition-api.vuejs.org/api.html#setup">文档说明</a></p>
    </li>
    <li>
     <b>组件封装：emit方法使用前需要先注册</b>
     <img src="https://user-images.githubusercontent.com/21302802/119456340-2b459f00-bd6d-11eb-8808-3ac727999e61.png" width="100%" />    
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
