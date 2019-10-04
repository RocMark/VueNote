# Vue Router 用途
1. 控制網址
2. 判斷是否登入
3. Cookie狀態

* router-link-active
<router-link to="/add" exact>Add</router-link>
可利用 這個去 Style 連結的樣式

# routes 兩種寫法
```js
  routes: [
    // 小型專案用此，會把所有 component 裝在同一支JS
    {
      path: '/comics',
      name: 'Comics',
      component: Comics
    },
    // 大型專案用此，會將 import 的包成一支 JS
    // webpack 的功能，非同步載入，換頁才載該支
    // code splitting 類似 Lazy Load
    {
      path: '/comics',
      name: 'Comics',
      component: () => import('@/pages/Comics')
    }
  ]
```

# VueRouter 使用預備
  * VueRouter 等同於 HTML8 History API
  * router-view 為路徑變更 要切換的區域 
  內容由 本體的 compo決定
  ```html
    <div id="app"> 
      <h1>頁面切換不受影響</h1>
      <!-- 可用路徑也可用名稱 -->
      <router-link to="/">Home</router-link>
      <router-link to="'home'">hello</router-link>
      <router-view></router-view>
    </div>
  ```
  ```js
    import router from './router'
    new Vue ({ router, })
  ```
<!-- -------------- -->

# VueRouter 本體
* 順序有差，從上到下檢查，越重要的放越前
```js
  const router = new VueRouter({
    routes: [ // 放所有需要的網址
      {
        path: '/', // url路徑
        name: 'list', // 路由名字 (調用方便)
        component: List, // 顯示的元件
      },
      {
        path: '/update/:id',
        name: 'update',
        component: Edit,
      },
      // 例外處理
      // 可透過 redirect 導回首頁 或 另外製作 404頁面
      {
        path: '*',
        redirect: '/',
      },
    ],
  })
```
<!-- -------------- -->

# VueRouter params參數
  * this.$route.params.name 
  對應 routes 該路徑的 name
  * this.$route.params.id
  利用 this.$route.params.id 取得 url 參數
  ```js
    data(){ id: this.$route.params.id }
    created(){ /* axios-get */ }

    routes: [
      path: '/blog/:id',
      name: 'singleBlog',
      component: singleBlog,
    ]
  ```
<!-- -------------- -->

# 動態連結
  * 切記必須使用 v-bind
  <ul v-for="post in posts">
    <li><router-link v-bind:to="'/blog/' + post.id"></li>
  </ul>
<!-- -------------- -->

# VueRouter 方法
  this.$router 有兩種方式 / 傳遞參數亦有兩種方法
  1. push 會產生記錄 可上下頁切換
  2. replace 不會產生記錄 不可上下頁切換

  # this.$route 差異 this.$router
  * $route 為 當前的路徑狀況
  因此需要取得網址參數使用此
  this.$route.params

  * $router 為 VueRouter
  若要做頁面切換使用此
  ```js
    this.$router.replace({ path: `/update/${id}` })
    this.$router.push({ 
      name: 'home', // VueRouter 中取的 name
      params: { id },
    })
  ```
<!-- -------------- -->


# 巢狀 Router
> http://bit.ly/2zereOl 

* routes 中 撰寫 children
有子層結構，在共用層要使用 redirect 指向某一個子層
* 必須 搭配 beforeEach
```js
  routes: [
    {
      path: '/main',
      name: 'main',
      component: main,
      redirect: '/main/index',
      children: [
        // 代表 /main 要共用
        // 
      ],
    },
  ],
```

# beforeEach
* 會建議使用 switch case 後續擴充會較佳
```js
  const router = new VueRouter({ ... })
  router.beforeEach(async (to, from, next) => {
    //...
    switch(to.name) {
      case 'news':
        await router.app.$store.dispatch('API', '/news')
        break
      case 'products':
        await router.app.$store.dispatch('API', '/products')
        break
      //...
    }
    next()
  })
```


# What is # in URL?
  > 網址上的 # 字號，需要由後端配合消掉
  > VueRouter 要設定成 mode: 'history'
  讓所有網址都會導向 index.html 
  再用 Router去控制網址呈現
  * localhost:8080/#/home
  不會向 Server 發送 request
  Ex: #top 會滾動到該 DOM 的位置
  * localhost:8080/home
  會向 Server 發送 request
<!-- -------------- -->

# hash # & history mode 差異
  美觀 以及 url 可讀性
  history mode 還需要 後端配合，
  否則有些頁面如 ~/users/id 就會返回 404
<!-- -------------- -->










# 安裝 Vue Router (未安裝 vue-router做法)
  1. 安裝 vue-router
  npm i vue-router -S
  2. 於 src 新增 router.js
  3. 於 main.js 新增 import router
  4. APP.vue 建立架構
  ```js
    import Vue from "vue";
    import Router from "vue-router";
    import Skills from "./components/Skills.vue";
    Vue.use(Router)
    export default new Router ({
      routes: [
        {
          path: '/skill/:name',
          name: 'skills',
          component: Skills
        },
        {
          path: '*',
          redirect: '/',
        },
      ],
    })
  ```
  * main.js
  ```js
    import VueRouter from 'vue-router'
    Vue.use(VueRouter)
    const router = new VueRouter({
      routes: Routes
    })
    new Vue({
      router,
    })
  ```
<!-- -------------- -->