# filter
> http://t.cn/Rdx6Hj8
filter 並不會改變原始資料

# filter computed method 比較
filter 用於資料格式化
* computed vs methods
computed用於邏輯計算，相依 data資料，有cache (效能較佳)
methods 用於狀態改變，無 cache，呼叫必重跑

# filter 用法
* 兩種使用方式
* filter可做 串連 & 代入參數
{{ msg | filterA | filterB('arg1') }}
<div :id="msg | filterName">

* 全域過濾 & 本地端過濾
```js
  Vue.filter('capitalize', function(val) {
  // 全域過濾
      return val.charAt(0).toUpperCase() + val.slice(1);
  });
  
  // 句尾點點點 {{ msg | truncateStr('lorem3', 6) }}
  Vue.filter('truncateStr', function(str, num) {
    const count = (num <= 3) ? num : num - 3
    const result = str.split('').slice(0, count).join('')
    if (num >= str.length) { return str }
    return `${result}...`
  });
  // 本地過濾
  filters: {
    toUpperCase(val){
      return val.toUpperCase()
    }
  }
```
# computed 用於較複雜的資料處理
computed 會從 data 取資料 具相依性
