# smart-rollcall
1141226手機板點名系統 - Deployed by EZPage
# 小清華專屬課後點名系統 (PWA)

**System Version**: 5.4 (Data Management)  
**Last Updated**: 2025-12-26

這是一個基於單一 HTML 檔案開發的輕量級 PWA (Progressive Web App) 點名系統，專為課後社團與加強班設計。具備多班級管理、Google/Email 雙重登入、LINE 瀏覽器自動跳轉引導，以及完整的請假審核與週報表功能。

---

## ⚠️ 安全性與權限重要說明

> **⛔ 強烈建議：請將此 GitHub Repository 設定為 Private (私人)，以免管理者密碼與學生個資外洩。**

### 🔑 管理者憑證
- **管理者 (老師) 登入密碼**: `admin123`  
  *(若需修改，請搜尋原始碼中的 `checkAdmin` 函式)*
- **網域限制**: 系統僅允許 `@ppsh.ptc.edu.tw` 結尾的 Google 帳號或信箱註冊登入。

---

## ⚙️ 部署流程 (Deployment)

本系統為 **Serverless Single File Application**，所有邏輯皆封裝在 `index.html` 中，依賴 Google Firebase 進行後端運算與儲存。

### 1. Firebase 專案設定
請至 [Firebase Console](https://console.firebase.google.com/) 建立專案並完成以下設定：

1.  **Authentication (驗證)**:
    - 開啟 **Google** 登入供應商。
    - 開啟 **電子郵件/密碼** 登入供應商。
    - **Settings > Authorized domains**: 務必將您的 GitHub Pages 網域 (例如 `frentexx.github.io`) 加入白名單，否則 Google 登入會失敗。
2.  **Firestore Database (資料庫)**:
    - 建立資料庫 (建議選擇 `asia-east1` 台灣機房)。
    - **Rules (安全規則)**: 建議設定為僅允許學校網域讀寫。

### 2. 程式碼配置
開啟 `index.html`，捲動至底部找到 `<script type="module">` 區塊，將 `firebaseConfig` 替換為您的專案設定：

```javascript
const firebaseConfig = {
    apiKey: "您的_API_KEY",
    authDomain: "您的專案ID.firebaseapp.com",
    projectId: "您的專案ID",
    storageBucket: "您的專案ID.firebasestorage.app",
    messagingSenderId: "...",
    appId: "...",
    measurementId: "..."
};
