# Vue 生命週期

## beforeCreate
- $el, $data, DOM 都未載入
- 用途: 展示 Loading 畫面
- 勿在此 Call API ，無論 API 回應速度，該回應還是會在 created 才被處理，因還未有 $data 可以儲存該資料
- server-side rendering 時會被呼叫
```js
  el: '#app',
  data(){ return { a: 123, } },
  beforeCreate() {
    console.log(this.a) // undefined
    console.log('$data 載入前')
  },
```

## created
- $el, DOM 都未載入，$data 已可使用
- 用途: 初始化資料、AJAX Call
- server-side rendering 時會被呼叫
```js
  data(){ return { a: 123, } },
  created() {
    console.log(this.a) // 123 (data 可被取得)
    console.log('$data 載入後，但 $el 還未載入')
  },
```

## beforeMount
- $data 已載入 (此生命週期較少用到)
- server-side rendering 時 不會 被呼叫
```js
  beforeMount() { console.log('還未掛載 DOM') },
```

## mounted
- $el, $data, DOM 皆載入
- 用途: 渲染畫面、掛載監聽器
- server-side rendering 時 不會 被呼叫
```js
  mounted() { 
    console.log('DOM 已可使用，在此做更動、渲染') 
  },
```

## beforeUpdate
- 當 相依資料更新、或需重新渲染 時觸發，在 DOM 重新渲染之前
- 此時為 修改資料的最後時機
- 用於 debugging 監控何時元件被重新渲染
```js
  beforeUpdate() { 
    console.log('在此可以取得已更新的資料')
    console.log('但新的 DOM 還未被渲染') 
  },
```

## updated
- 當 相依資料更新、或需重新渲染 時觸發，重新渲染 DOM 之後
- 在此取得已更新的 DOM 
```js
  updated() { console.log('新的 DOM 已渲染完成') },
```

## beforeDestroy
- watchers / 子元件 / 事件監聽 被摧毀之前
- 此時 元件還是可以正常運行
- 用途: 在此清除 事件監聽、訂閱資料
```js
  beforeDestroy() { alert('你確定要刪除') },
```

## destroyed
- 解除 watchers / 事件監聽 / 清除子元件 之後
- 可用來告知 伺服器，此元件已被清除
```js
  destroyed() { console.log('該實例已被摧毀') },
```
 
## 參考資料
- [Understanding Vue.js LifeCycle Hooks](https://alligator.io/vuejs/component-lifecycle/)
- [詳解vue生命週期](https://segmentfault.com/a/1190000011381906)