# Vue Event Bus (中繼站)
- 用於多個元件不相干，但需要同一個狀態
- 第三者 用來 傳遞事件 給 各元件
- 要注意的事，$emit 是否會打到同名事件
- 解: 製作多個 Bus，但剛結構更複雜，選用 Vuex 會更佳
```js
  // event bus
  const bus = new Vue()

  // 元件 A
  methods: {
    onClick(){
      // 由 元件 A 發送 $emit 事件給 bus
      bus.$emit('receive', this.msg)
    }
  }

  // 元件 B
  created(){
    // 元件 B 於 created 註冊 receive 事件
    const that = this
    bus.$on('receive', function(newMsg) {
      that.msg = newMsg 
    })

    // 可用 ES6 箭頭函式 直接取外層 this (免 that)
    bus.$on('receive', (newMsg) => {
      this.msg = newMsg 
    })
  }
```