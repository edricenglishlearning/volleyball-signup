# 財管系排球兄弟姐妹盃｜線上報名

- 報名網頁：`index.html`（放在 GitHub Pages）
- 後端與資料庫：`apps-script/Code.gs`（Google Apps Script + Google 試算表）

## 一、更新 Apps Script（後端）

1. 打開原本的 Apps Script 專案，把 `Code.gs` 全部換成 `apps-script/Code.gs`，確認 `SHEET_ID` 已填入試算表 ID。
2. 左邊的 `Index.html` 可以刪掉（網頁改放 GitHub 了）。
3. 存檔（⌘ + S）。
4. 「Deploy → Manage deployments → 鉛筆 → Version 選 New version → Deploy」。
   - 執行身分：我（Me）
   - 存取權：所有人（Anyone）
5. 複製「Web app URL」，格式是 `https://script.google.com/macros/s/……/exec`。

## 二、放上 GitHub Pages（前端）

1. 打開 `index.html`，找到最上方這行，把網址換成剛剛複製的 Web app URL：
   `var API_URL = 'https://script.google.com/macros/s/請貼上部署網址/exec';`
2. 登入 GitHub → 右上角「＋ → New repository」，名稱例如 `volleyball-signup`，選 **Public**，按 Create。
3. 在新 repo 頁面點「uploading an existing file」，把 `index.html` 拖進去，按「Commit changes」。
   （`apps-script` 資料夾與這份 README 不需要上傳。）
4. 到 repo 的「Settings → Pages」：Source 選「Deploy from a branch」，Branch 選 `main`、資料夾 `/ (root)`，按 Save。
5. 等 1～2 分鐘，頁面上方會出現網址：`https://你的帳號.github.io/volleyball-signup/`，這就是報名網址。

之後修改網頁，只要在 GitHub 上重新上傳 `index.html` 即可；修改 `Code.gs` 則要在 Apps Script 建立新版本部署（網址不變）。

## 三、安全性

- 網頁原始碼是公開的，但裡面沒有任何密碼或金鑰；API 網址被看到也只能「新增報名」，讀不到任何資料。
- 試算表不公開分享，只有擁有者看得到。
- 所有欄位與金額都由 Apps Script 重新驗證、計算；並有防公式注入、防重複送出、防機器人與流量上限。
- 瀏覽器呼叫 API 時不帶 Google 登入 cookie，Safari 或登入多個 Google 帳號都能正常使用。
