# Vue 元件

# 大綱
- 載入元件
- Vue props 父傳子
- Vue props 型別檢查
- 子傳父

# Vue 資料傳輸
* Props in, Events out
* 使用 props 由 父傳給子
* 使用 $emit 由 子傳給父

# 載入元件
- 於 components 建立元件 (props 接容器傳來的參數)
- 於 容器中 import 該元件
- 於 components 寫上要使用的元件名
- 於 HTML 撰寫 該元件 & 要傳的參數
```js
  // template
  <HelloWorld msg="Welcome to Your Vue.js App"/>

  // script
  import HelloWorld from '@/components/HelloWorld.vue'

  export default {
    name: 'home',
    // 於此撰寫此容器要用到的元件
    components: {
      HelloWorld,
    },
  }
```

# Vue props 父傳子
- props 用於元件間傳值
- props 盡可能將型別、限制寫細
- 不符合 validator 會噴錯
```js
  // 父元件
  data(){
    return { msg: 'Msg From Parent' }
  }

  // 利用 v-bind 綁定資料 傳遞給子元件
  // 屬性使用 - kebab case
  <template>
    <child-compo :parent-msg="msg" ></child-compo>
  </template>

  // 子元件 使用 小駝峰
  props: ['parentMsg']
```

# Vue props 型別檢查
```js
  props: {
    propA: null, // 不檢查型別
    propB: Number, // 限定數字
    propC: [String, Number] // 字串或數字
    obj: {
      type: Object, // 可接受 物件 或 陣列
      default(){   // 預設物件
        return {
          msg: 'Hey'
        }
      }
    }
    src: {
      type: String,
      required: true,  // 是否為必要
      default: 'test', // 預設值
      validator(val) {
        // 檢測值必須為陣列中的某個值
        return ['test', 'a'].indexOf(val) !== -1
      },
    },
  },
```

# Vue $emit 子傳父
- 子元件 透過 @click 觸發 $emit 事件給 父元素
- 父元素 於 mounted 掛載監聽器監聽 $emit 的指令
- 父元素 接受到 $emit 事件 執行對應的 Function 更改自身data
- [六角學院 Kuro Hsu](https://www.youtube.com/watch?v=T2JsTE0Hq58&t=4990s)
```html
  <!-- 子元件 template -->
  <button @click="updateText"></button>
  <input v-model="msg">
```
```js
  // 子元件
  props: { parentMsg: String },
  data(){ return { msg: this.parentMsg } },
  methods: {
    updateText(){
      // 使用 this.$parent 取得父元件
      // update 為自訂指令名
      this.$parent.$emit('update', this.msg)
    }
  }
```
```js
  // 父元件
  data(){ return { msg: 'Hey' } }
  methods:{
    selfUpdate(val){
      // 接收到 $emit 事件 將其值覆蓋 父元件 data
      this.msg = val
    }
  }
  mounted(){
    // update 自訂指令名 後為 call methods
    this.$on('update', this.selfUpdate)
  }
```
