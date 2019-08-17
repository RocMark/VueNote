# FireBase

# 連接 FireBase
- [FireBase](https://firebase.google.com/)

# 建立 FireBase 專案
- 右上角進入主控台 / Console
- 新增專案
- Hosting / 開始使用

# 本地建立專案
- 安裝 npm 套件
- firebase login 登入 Google
- firebase init  啟動專案
- firebase deploy 部署網站
```
  npm i -g firebase-tools
  firebase login
  firebase init
  firebase deploy
```

# firebase init
- 注意 Vue 專案輸出夾為 dist
```
  firebase init
  // use public ?      dist
  // single-page app?  Yes
  // over write html?  Yes
```

# 與 firebase 網站連接專案
- firebase use --add
- 可在 firebase.serc 確認是否連接到該專案
```
  firebase use --add
  // project?  建立的專案id
  // alias?    staging
  {
    "projects": {
      "default": "VueFireBase"
    }
  }
```

# firebase 上線
- init 完後 npm run build 建立輸出內容
- firebase deploy
- Hosting URL: ~.firebaseapp.com
```
  npm run build 
  firebase deploy --only hosting
```