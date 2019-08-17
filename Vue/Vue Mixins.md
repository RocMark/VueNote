# Vue Mixins
* 將可複用的 Code抽出到 Mixin File 在做 import

#38 Mixin
建立 mixins 資料夾 > searchMixin.js
```js
  // 於 compo 使用
  import searchMixin from '../mixins/searchMixin'
  mixins: [ searchMixin ]
  this.$_searchMixin_test()

  // searchMixin 內容
  export default Vue.mixin({
    method: {
      $_searchMixin_test(){ console.log('test') }
    }
  })
```

## 屬性命名規則 Plugin & Mixins
* 注意命名方法 $_searchMixin_test()
建議加上 該 Mixins 名稱當做前墜
避免跟其他 Mixins / 元件 methods 搞混

## 屬性命名規則Mixin 用法
* 注意點 !!!!!!!
> 當載入 Mixin 後  載入的 LifeCycle 程序 也會執行
來自 Mixins 的 會先執行 !!!

> 如果 Mixin 與 元件中 有同名 Function
* 元件中的 Function 優先權較高

```js
  // 在元件中 加上 mixins 屬性
  mixins: [myMixin, myMixin1],

  // 會把下面兩個特性都導入該元件
  const myMixin = {
    created(){ this.$_myMixin_hello() },
    methods: {
      $_myMixin_hello(){ console.log('Hello') }
    }
  }
```