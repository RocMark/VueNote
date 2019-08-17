# Vue
框架強調資料，資料驅動

# SEO
SPA 補上一段 Server Side Render (SSR) 較佳

# Vue
Vue 可選擇控制某塊，並不是整個網站都需要用 Vue
可使用 jQuery 配 Vue
* jQuery 去撰寫需要動畫的部分
* Vue 去撰寫資料相關

# Vue 資料控制 Dom
scroll position 
當資料改變時，滾動卷軸
* this.$el 可找到該元件的最外層

# 座標系統 
* 重點於 原本座標 & 內外層座標關聯

# PageHeader & PageFooter
<router-view style="padding:60px 0 40px 0;"></router-view>

PageHeader & PageFooter 用 Fixed
要用 router-view 把原本的位置撐開

# Tips
* v-for="(val,key) in obj"
* 勿拿 index 來刪除資料，使用 id 較準確

* 使用 v-model 實現雙向綁定資料
newUserName 對應到 data 中的 newUserName
<input v-model="newUserName">

# Refs
取得該元素
<input type="text" ref="input">
methods 中 利用 this.$refs.input 取得
this.$refs.input.value 可取值

# 觀念
* 雙向綁定 (免去事件監聽 v-model 榜表單)

* Template
Vue 的 雙括號為 innerText
* 要用 HTML 應使用 v-html=""
* Vue 中的 this 會指向 new 的實體
常用 箭頭函式 去避免產生新的 this
Ex: this.computed

# computed
用於需要處理的資料
1. 用 v-bind 綁定 input & data(){keyWord:''}
2. 當 user 輸入資料，data() 中 keyWord 改變
3. keyWord改變，連動到 computed 中有使用到 this.keyWord 的 Function
4. 當 含 this.keyWord 的 Function 變動，呼叫該 Function 的 Function 也會重新運行 
Ex: filterArray()

# 模板概念
* {{}} 對應到 innerText
* v-html 較少用了
如果是自己產的沒問題，
若從其他地方取來的，容易被串改，盡量避免
* v-html="highLight(傳入變數)" 對應 innerHTML
highLight 為 method 中的 Function
該 Function return htmlStr

* 使用 HTML <template>
v-if="此處撰寫判斷式"
v-else="此處撰寫判斷式"

v-for="city in filterArray"