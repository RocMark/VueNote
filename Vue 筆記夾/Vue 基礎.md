# Vue JS

# 大綱
- Vue 建立實體
- Vue Template 使用
- Vue 資料 (data, computed)
- Vue 方法 (computed vs method)
- Vue 監聽 (computed vs watch)
- Vue v-if / v-show (渲染/顯示與否)
- Vue v-for (迴圈)
- Vue v-model (雙向綁定)
- Vue v-on (事件綁定)
- Vue v-bind (屬性綁定)

# Vue Instance 
- 建立 Vue 實體
- 指定整個 Vue 內容的容器 #app
```js
  // <div id="app"></div> 作為根元素

  // 建立 Vue 實體
  const app = new Vue({
    el: '#app',       // 掛載 Vue實體的元素
    data(){return{}}, // 綁定的資料
    computed:{},      // 用來 經過運算 的 資料
    props:{},         // 用來接收外部資料的屬性
    methods:{},       // Vue 實體內用的函式
    watch:{},         // 偵測 Vue 實體內的資料變動
    components: {},   // Import 使用的子元件
    template: ''      // Vue 編譯的樣板
    mounted(){},      // Vue LifeCycle
  })
```

# VueCli 中的 實體
- [render 簡寫過程](https://bit.ly/2M2MqMW)
```js
  new Vue({
    router, // VueRouter
    store,  // Vuex
    // createElement 的簡寫 (用於產生 DOM)
    render: h => h(App),
    // mount 時渲染 掛載到 根節點上
  }).$mount('#app')
```

# Vue Template
- {{ }} 可帶入 data,computed 變數
- {{ }} 內部可做運算，但建議用 computed儲存，較易管理
```html
  <p> 純字串 </p>
  <p> {{ 變數 }} </p>
  <p> {{ score * 0.8 }} </p>
```

# Vue 資料 (data, computed)
- data  用於純資料
- computed 用於需要計算的值
- props 用於元件間傳值 (詳於元件篇)
```js
  <p>{{this.sum}}</p>

  export default {
    name: 'home',
    data() {
      return {
        nums: [1, 2, 3, 4, 5],
      }
    },
    computed: {
      sum() {
        return this.nums.reduce((sum, el) => sum + el, 0)
      },
    },
  }
```

# Vue 方法 (computed vs method)
- computed 用於純邏輯運算，當相依資料變更才更新
- method 只要有資料變更即更新 (每次都會更新，須注意效能)
```js
  data(){
    return { name: 'tim'}
  }
  computed: {
    upperName(){ return this.name.toUpperCase() }
  },
  methods: {
    getNow() { return Date.now() }
  }
```

# Vue 監聽 (computed vs watch)
- Vue computed

# v-if / v-show (渲染/顯示與否)
- v-if  是否渲染 DOM 元素 (false 連 DOM 都不產生)
- v-show 會渲染 DOM 元素 (display: none)
- 時常開關的使用 v-show 較節省資源 (省去產生 DOM)
- 有判斷式建議寫在 computed 中 
```html
  <!-- 可用 ! 使 Boolean 反轉 -->
  <!-- v-if 為 false 連 DOM 都不產生 -->
  <ul v-if="hidden"></ul>

  <!-- 有判斷式建議寫在 computed 中 -->
  <ul v-if="score >=60 "></ul>

  <!-- v-show 會產生 DOM，差別於 display: none 與否 -->
  <ul v-show="hidden"></ul>
```

# v-for (迴圈)
- v-for 寫在要重複產生的元件上
- StyleGuide 會建議 v-for 有使用 v-bind:key
- 簡而言之: 給予 key 在進行排序時，就不需要銷毀 DOM，以達重複利用、節省資源。
- [VueStyleGuide 講解](https://cn.vuejs.org/v2/guide/list.html#%E7%BB%B4%E6%8A%A4%E7%8A%B6%E6%80%81)
```html
  <ul>
    <li v-for="(item, index) in items" :key="item.id">
      {{ item }}
    </li>
  </ul>
```

# v-model (雙向綁定)
- 當 input 內容變更 p 內容也會更著變更
```js
  <input v-model="inputUrl">
  <p>{{ inputUrl }}</p>
```

# v-on (事件綁定)
- 使用 @ 做為縮寫
```html
  <input v-on:click=""> 
  <!-- .prevent 代表 event.preventDefault() -->
  <!-- .stop 代表 event.stopPropagation() -->
  <input type="submit" @submit.stop.prevent> 

  <!-- 鍵盤事件 -->
  <input @keyup.enter="onEnter">
  <input @keyup.13="onEnter">

  <!-- 滑鼠事件 left,right,middle 2.2.0版本 -->
  <button @click.left="onLeftClick">

  <!-- 只觸發一次 -->
  <input @click.once="once">

  <!-- 僅通過自身觸發，冒泡傳遞的不觸發 -->
  <input @click.self="self">

  <!-- 代入參數 & eventObject-->
  <button @click="myFunc(name,$event)"> 
  
  data(){ return{ name:'test' } }
  methods: { myFunc(name, e){} }
```

# v-bind (屬性綁定)
```html
  <a :href="" >
```