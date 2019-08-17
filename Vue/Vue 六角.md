# Vue.js 教學
> https://quip.com/N3iKAEDJEVmD

# Vue文件
> https://cn.vuejs.org/v2/guide/installation.html

//? Vetur VSCode推薦插件

# 簡易比較
jQuery 用 DOM元素來觸發功能、設計動畫效果
vue、ng、react 資料驅動功能

# 安裝
* 開發版本，完整警告提示
* 生產版本，壓縮無警告
* CDN

# 特性
* WebComponent
* 數據驅動內容
* 利用屬性判斷相關邏輯
* this指向 data內容

# 撰寫樣本渲染
```js
    <div id="app">
        {{message}}
        {{score *0.8}}
    </div>
    let app = new Vue({
        el:"#app", // element綁定
        data: {
            message:"hello world", 
            score: 60
        },
    })
```

# ESLint SetUp
//? .eslintrc檔案 & npm
```js
    npm install eslint eslint-plugin-vue 
    "extends": [
        "plugin:vue/essential"
    ],
```

# 指令 v-if v-show 比較
//* v-if => true才渲染，false連標籤都不產生
//? v-show => false時，inline style display:none
```js
    <div id="app">
        <div v-if="loading">訊息載入錯誤</div>
        <div v-show="show">保留DOM元素</div>
    </div>
    let app = new Vue({
        el:"#app",
        data: {
            // <div v-if="loading">訊息載入錯誤</div>
            //? v-if 為 true 才會顯示出來
            score: 0,
            loading: true,
        },
    })
```

# v-if / v-else
//* 可用兩個if 或 if後 else
```js
    <div id="app">
        <div v-if="score>=60">不合格</div>
        <div v-else="score<60">不合格</div>

        <div v-if="score>=60">合格</div>
        <div v-if="score<60">不合格</div>
    </div>
        let app = new Vue({
        el:"#app",
        data: {
            score: 0,
        },
    })
```

# v-model="message" //! 雙向資料綁定 強大
//? 修改 Input數據時，即時變更JS中 data的值
//* 變更後並渲染

> 注意帶入的型態 數字 => number String => text
> 否則不會顯示
```js
    <input type="number" v-model="currency">
    <h1>{{currency*0.25}}</h1>
    <h1>{{currency*30}}</h1>
```

# v-for 迴圈
//* 類似 PUG 寫法 
//? v-for="color in colors" {{color}}
```js
    <ul v-for="color in colors">
        <li><a href="#">{{color}}</a></li>
        {{family.father}}
        {{family.mom}}
    </ul>

    data: {
        colors:["red", "blue", "yellow"],
        home:[
            {father:"tom", mom:"May"},
            {father:"Joe", mom:"Marry"},
        ]
    },
```

# v-on 綁定事件
//* v-on 可用 @ 作為縮寫
//! 只觸發一次 @click.once
> 停止冒泡 & 阻止默認行為
//? button @click.stop.prevent
```js
    //? input @keyup.enter="onEnter" // 鍵修飾符
    // input @ keyup.13="onEnter" //鍵代碼

    <h1 id="title" v-on:click="myFa(num)">{{num}}</h1>
    data:{
        num: 123456
    },
    methods:{
        myFa:function (num) {
            alert(num)
        }
    },
```

# v-bind 資料綁定動作

```html
<img  v-bind:src = "imageSrc">
<img  :src = "imageSrc">  //* 縮寫
<a  :href = "url">  
<img  :src = "'/path/to/images/' + fileName">
<div  v-bind = "{ id: someProp, 'other-attr': otherProp }"> </div>
```

# v-html
將內容渲染成 HTML格式

# watch //! 監聽改動
```js
    <input type="radio" 
            :value="branch"
            v-model="currentBranch"
            >

    watch: {
        //? 更動 currentBranch 執行 fetchData Func
        currentBranch: 'fetchData'

        //* 寫法效果同上
        currentBranch: function(){
            this.fetchData()
        }
    }
```



# Computed
//* 用於運算邏輯較重
//? 把於HTML的運算邏輯搬到 JS computed 屬性

//* 常用來判斷目前網頁狀態

* 收納 template 邏輯 即時更動資料靠此

//! 牽動到data 才會更動
> 在computed中必須要使用到 this.x 監聽該資料更動，才會生效
```js
{{ fullName}}
computed: {
    fullName() {
        //* 當 fName或 lName 改動就會自動重新 render
        return this.fName + '' + this.lName
    }
}
```

# Method & Computed 差異 //* 重要
//! Computed 無法帶參數，Method可

//? 不確定每次都會更新，請用 Computed (運算邏輯)
//* 確定每次都會更新，用 Method (AJAX)

# Why Use Computed
於效能上較佳，資料未更動就不會作重新渲染
具有資料緩存的功能 (記錄到記憶體)

# Computed 範例
```js
    // HTML  {{japan}}
    // HTML  {{now}}
    let app = new Vue({
        el: '#app',
        data: {
            NT: 0 // 當此値更新 japan return值更動
        },
        computed: {
            japan() {
                return this.NT * 0.2713
            },
            now() {
                let x = this.a // 當 a更動時回傳當下時間
                let date  = new Date()
                return date.getSeconds()
            }
        },
    })
```

# Method 用法
> 用於 AJAX 這種一定需要更新頁面的
```js
    // {{changeA(1)}}
    let app = new Vue({
        methods(){
            changeA(num){
                return 'a' + num
            }
        }
    })
```