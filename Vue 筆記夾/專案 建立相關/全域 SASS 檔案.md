# 全域 SASS 檔案

# 安裝套件
- Vue UI 新增套件 sass-resources-loader
```
  vue-cli-plugin-sass-resources-loader
```

# 建立設定
- 自行建立 vue.config.js 檔
- @ 代表 /src，路徑需要自行修改
```js
  module.exports = {
    css: {
      loaderOptions: {
        sass: {
          data: `
            @import "@/scss/_variables.scss";
            @import "@/scss/_base.scss";
          `,
        },
      },
    },
  }
```

# 參考資料
- [Globally Load SASS into Vue.js](https://vueschool.io/articles/vuejs-tutorials/globally-load-sass-into-your-vue-js-applications/)