# Vue 風格指南速覽

# Class A 必要
- 元件名 以多單詞組成
- data 使用函式 data(){return ~}
- props 盡量詳細
- v-for 配合 v-bind:key (效能)
- 避免 v-if & v-for 用在同元素
- 為元件設置作用域 (style="" scoped)
- 私有屬性名 (以$_做為開頭)

# Class B 強烈推薦(可讀性)
- 元件命名相關整理
- 自閉合元件


# 元件名使用 多個單詞組成
> Ex: todo-item
- 為了避免與現有、未來的 HTML元素衝突
- 注意 寫於元件時，以大駝峰表達
```js
  export default {
    name: 'TodoItem',
  }
```

# data 使用 函式
- 物件傳址，使用物件會造成使用同樣的元件時，引用了同一份資料。
- 使用函式就可以讓元件產生各自的物件做使用。
```js
  export default {
    data() {
      return {
        nums: [1, 2, 3, 4, 5],
      }
    },
  }
```

# prop 定義
- 容易維護、測試
- validator 不符合時會警告
```js
  props: {
    src: {
      type: String,
      required: true,
      default: 'test',
      validator(val) {
        // 檢測值必須為陣列中的某個值
        return ['test', 'a'].indexOf(val) !== -1
      },
    },
  },
```

# v-for 配合 v-bind:key
- 給予 key 在排序時，即不會刪除舊有的 DOM，而是移動，省去了重新渲染的資源。
```html
  <ul>
    <li v-for="(num, index) in nums" :key="num.id">
      Index: {{ index }} Value : {{ num }}
    </li>
  </ul>
```

# 避免 v-if & v-for 用在同元素
- v-for 優先級 高於 v-if
- v-for 先做但有些並不會被渲染，而造成資源浪費
- 情況1: 過濾表單 (應先於 computed filter後再 v-for更佳)
- 情況2: 避免渲染本該隱藏的表 (將 v-if 放置外層容器，可達同效果)

# 為元件設置作用域
- 使用 scoped / CSS Modules / BEM 
- 避免衝突 & 團隊內理解
<style scoped></style>
<style module></style>

# 私有屬性名 (以$_做為開頭)
- Vue 使用 _ 來定義私有屬性，可能衝突
- Vue 使用 $ 作為給用戶的實例屬性，亦不適合當開頭
- Vue 推薦將兩者前墜結合 $_ 做為私有屬性，避免衝突
```js
  // 使用 $_ 表該 method 為私有
  var myGreatMixin = {
    methods: { $_myGreatMixin_update() {} }
  }

  // 甚至更好！
  var myGreatMixin = {
    methods: {
      publicMethod() {
        myPrivateFunction()
      }
    }
  }
  function myPrivateFunction() {}
```


# ClassB 元件命名相關
- 元件名 統一 大駝峰 或 kebab-case
- 各元件分成獨立文件 (多元件不要寫在同一個檔)
- 基礎的元件名 (給予前墜)
- 唯一的元件名 (使用 The 前墜 TheFooter)
- 相關聯的元件名 (使用 父元件名 當前墜)
- 元件名單詞順序 (統一即可 Ex: 類別、元件、動作/狀態)

# 基礎元件名 (無邏輯 & 狀態 僅展示用)
- 更易於尋找這些常用到的元件名
- 這些元件不包含全域狀態 Vuex (盡可能單純)
```
  components/
  |- BaseButton.vue  // 基礎元件
  |- AppNav.vue      // 網站共通
  |- VIcon.vue       // 某框架樣式
```

# 唯一的組件名
- 使用 The 前墜
- 代表該頁面只使用一次
- 通常用於 Nav / Header / Footer

# 相關聯的元件名
- 不建議使用資料夾嵌套 (難以搜尋、過於巢狀)
```
  components/
  |- TodoList.vue
  |- TodoListItem.vue
  |- TodoListItemButton.vue
```

# 元件名單詞順序
- 統一單詞順序 Ex: 類別、元件、動作/狀態
```
  components/
  |- SearchButtonClear.vue
  |- SearchButtonRun.vue
  |- SettingsCheckboxTerms.vue
```

# 自閉合元件
- 