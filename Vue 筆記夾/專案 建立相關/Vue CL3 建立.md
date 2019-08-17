## Vue CL3 建立

## 建立專案
- vue init webpack-simple 專案名 (Vue CLI 2.0)
- vue create 專案名 (Vue CIL 3)
```
  // 確定是否有安裝 node
  node -v
  // 安裝 cli
  npm i -g @vue/cli
  // 建立安裝
  vue create 專案名
```

## Vue UI
- 可以用 GUI 方式來建立專案
- 亦可匯入以建立好的專案，在進行一些設定調整
- 可以查看更多 指令執行的數據 (時間、大小...etc)
- 可以搜尋需要的插件並加入 (vuetify...etc)
```
  // 即會開啟於 http://localhost:8000
  vue ui
```

## 設定檔總覽
- package.json (npm 設定檔)
- postcss.config (postcss 設定檔)
- babel.config (babel 設定檔)
- .browserslistrc (設定 瀏覽器的支援度要到哪)
- .editorconfig (設定 coding style)
- .eslintrc  (ESLint 規則設定檔)
- .gitignore (Git 忽略不追蹤的檔案列表)

## 加入 Plugin 
- @vue/cli-plugin-* 插件名必須為此格式
```
  // @vue/cli-plugin-vuetify
  vue add vuetify
```

# 套件總覽

# Instant Prototyping
- @vue/cli-service-global
- 用來運行單一元件 不需要建立專案
```
  npm i -g @vue/cli-service-global
  vue serve online.vue
```

# postcss
> https://cythilya.github.io/2018/08/10/postcss/

## 參考資料
- [The Net Ninja](https://bit.ly/2Zv12Hi)