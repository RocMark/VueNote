# 主講 Vuex 
> https://www.youtube.com/watch?v=eX54AJFzxXU
(16:00 始 前面介紹 Gulp+WebPack架構)

# Vuex 功用
* 主要是用來 跨元件的

# Vuex 最常用於 會員登入
會員是否 登入的狀態 & 會員等級 會影響很多組件的樣版

# Store 本體
* 將 store.js 放在 src 當中
* 開發時，開啟嚴謹模式
* 上線時，關閉嚴謹模式，此模式非常耗資源
```js
  export default new Vuex.Store({
    state,
    getter,
    actions,
    mutations,
    // 開啟嚴謹模式
    strict: true,
  })
```
# Vuex 主要概念
* State
存放要共用的變數
* Getter
  官方建議不要直接用程式碼取 State的變數
  ```js
    // 不建議此法
    this.$store.state.showLoading

    // 建議此法 先將 Getter 寫於 state 的檔案中
    computed: {
      // ... 表 rest params
      ...Vuex.mapGetters([ 'showLoading', 'isLogin' ])
    }
    const getters = {
      showLoading: state => state.showLoading,
      isLogin: state => state.isLogin,
      userName: state => state.userName,
    }
  ```
<!-- ------ -->
* Mutation
  Mutation 必須是同步函式
  ```js
    const mutations = {
      isLogin(state , value) { state.isLogin = value }
    }
    // 不推薦 
    this.$store.commit('showLoading', true)
    // 推薦
    methods: {
      ...Vuex.mapMutations(['showLoading'])
    }
  ```
<!-- ------ -->
* Actions
  Actions 是非同步函式，只能 return Promise

  action 當中不應該直接修改 state 值 (會報錯)
  要先呼叫 mutations，利用 mutations 去改 state
  ```js
    const actions = {
      showLoading( {commit}, value ){
        // commit 會呼叫 mutations 中的 showLoading
        commit('showLoading', value)
      }
      login( {commit}, value ){
        return new Promise(resolve => {
          commit('showLoading', true)
          console.log('action login', email, pwd)
          // axios-get
        })
      }
    }
  ```
<!-- ------ -->

# 撰寫 Getter
> http://bit.ly/2tX3p8H 
Vuex 允許我們在 Store中定義 getter (可當成 store 的 computed屬性)
同 computed 依賴會被緩存，改變才重計算
```js
  // 呼叫
  this.$store.getters.doneTodos

  // Store 本體
  const store = new Vuex.Store({
    state: { ~ },
    getters: {
      doneTodos: state => state.todos.filter(todo => todo.done)
    }
  })
```

# 元件內使用 Getter
```js
  import {mapGetters, mapActions} from 'vuex';
  computed: {
    // 會產生一個 叫 showLoading 變數
    // 並監聽 State 的 showLoading
    ...mapGetters([ 'showLoading', 'isLogin' ])
    loginLabel (){
      return this.isLogin ? "login" : "logout"
    }
  }

  methods: {
    // 載入 actions 中的 login 函式
    ...Vuex.mapActions(['login'])

    async submitHandler(){
      let email = this.email
      let pwd = this.pwd

      // 此處的 this.login 會執行 actions 中的 login 函式
      // async await 會等待該行執行完 才跑下一行
      let res = await this.login({ email, pwd })

      if (res.status === 'ok') {
        let redirect = this.$route.query.redirect || "/"
        console.log(redirect)
        this.$router.replace(redirect)
      }

    }
  }
```