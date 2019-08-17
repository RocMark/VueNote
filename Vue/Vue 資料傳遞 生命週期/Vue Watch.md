# Vue Watch

watch: {
  // this.$nextTick(() => {})
  fn() {},
},

# computed VS watch
* computed 
> 初始值會自動計算
監控值，並修改值回傳 (重點在資料)
* watch 
> 初始值需手動設定
用於監控值，並執行對應 Function (重點在於 Func處理內容)

# Watch 過程
* Vue 中的 DOM更新為 非同步的!

Vue 先更新資料，更新完資料後，被 Watch捕捉
* Watch 的階段在 資料更新後 & 畫面/DOM 更新前 之間

* 如果在 Watch 中 有抓 DOM的動作要注意!
由於 watch 在  畫面/DOM 更新前，
所以如果要抓 Ex: li.active 會抓到不正確的 Dom

# 使用 this.$nextTick 使用時機
1. created() 中 有需要使用到 Dom 的操作
都應該放在 Vue.nextTick() 中，
或是將 Dom操作的部分 改在 mounted() 中撰寫
2. 當操作需要用到 "隨數據改變" 的 DOM時
為了確保在 畫面/DOM 更新完後才執行

```js

  const ul = this.$el.querySelector('ul')
  this.$nextTick(() => {
    // 資料改變後，給予 active class
    // 使用 nextTick 確保 畫面/DOM 更新後，才取得正確的 DOM
    const li = this.$el.querySelector('li.active')
    // do stuff
  })
```