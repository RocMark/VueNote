# Vue CSS
scoped 該 css 只作用該檔案的 template內容
* 若 css 內容過多可以載入外部 css 
<style src="./Skills.css" scoped> </style>

<div :class="{ alert: showAlert, 'bigFz': bigFz }">123</div>

# Best Way !
<div :class="alertObj">123</div>
alertObj 寫於 data 統一管理

```js
  data(){
    return {
      alertObj: {
        bigFz: true,
        showAlert: true
      }
    }
  }
```

# 亦可直接設置 style
* 注意 需要使用 camelCase
<!-- 亦可使用 style 去做設置 同上 -->
<div :style="{ backgroundColor: bgColor, fontSize: styleObj.divFz }">123</div>


#20 scoped css
1. 將全域 style 寫於 root
Ex: normalize & base & var

* 注意!! component style 會覆蓋於 上層 style
改寫成 scoped 要手動刷新一次

scoped 只作用於該元件，並附蓋掉其他來源設定
<style lang="sass" scoped>
  h1 { color: red; }
</style>

## scoped 原理
vue 會給予該物件 data-v-編碼
h1[data-v-160ar736]{ color: red; }