# 專案目的 (Project Purpose)
這是一個基於純前端技術 (HTML/CSS/JS) 的「最強編劇大考驗 / 無腦劇情互動」遊戲框架。
專案核心機制為「多網頁跳轉 (Multi-page routing)」，不依賴 JSON 資料庫，而是由多個獨立的 HTML 檔案組成劇情與測驗節點。
本文件的目標是讓 AI 能夠根據使用者提供的「任何影劇大綱或文本」，自動將其改編成一系列帶有趣味問答的 HTML 遊戲網頁，藉此考驗玩家對劇情的記憶力或吐槽功力。

# 網頁整體風格 (Design & UI Style)
- **視覺基調：** 明亮、乾淨且帶有日系手帳感的結構化 UI 介面。
- **色彩配置：** 採用淺木質調 (Light Wood) 元素。背景為米白色 (`#FDFBF7`)，主容器為純白 (`#FFFFFF`) 搭配淺木色邊框 (`#E6D5B8`)。文字統一使用深咖啡色 (`#4A3F35`) 以利閱讀。
- **排版結構：** 畫面置中對齊，主容器最大寬度設定為 `800px`，確保跨裝置的響應式閱讀體驗。

# 檔案命名與放置規則 (File Naming & Structure)
所有新生成的劇情節點必須放置於專案根目錄，並嚴格遵守以下命名規範：
- `index.html`：遊戲首頁 / 標題畫面。
- `node_[劇情名稱].html`：一般劇情推進節點（例如 `node_first_meeting.html`）。
- `quiz_[測驗名稱].html`：針對劇情細節提問的選擇題節點（例如 `quiz_water_splash.html`）。
- `ending_[結局名稱].html`：答錯被開除、或順利完結的結局頁面（例如 `ending_fired.html`）。
- `css/style.css`：全域共用的樣式表。

# 頁面結構與新增內容格式 (Page Structure & Content Format)
AI 生成的 HTML `<body>` 內必須包含以下核心結構，且 class 命名不可更動：
1. `<div id="scene-image" class="scene-container">`：放置情境標題。
2. `<div id="dialogue-box" class="dialogue-container">`：
   - 角色名稱標籤：`<h3 class="char-name">`
   - 對話或劇情文本：`<p class="text-content">`
3. `<div id="choices-container" class="choices-wrapper">`：
   - 選項按鈕：`<a href="目標檔名.html" class="choice-btn">選項文字</a>`

# AI 開發與劇情改編規則 (Rules for AI Assistant)
1. **劇情測驗自動生成：** 當使用者提供一段劇情文本時，AI 必須從中萃取關鍵細節（如人名、物品、荒謬台詞），並自動在劇情節點之間穿插 `quiz_***.html` 進行提問。
2. **選項與路由設定：** 
   - 測驗頁面需提供 3 到 4 個選項（包含一個正確答案與數個荒謬的錯誤答案）。
   - 正確選項的 `href` 必須導向接續的 `node_***.html`。
   - 錯誤選項的 `href` 必須導向搞笑 Bad Ending 頁面（例如「收視率慘跌」、「你被踢出編劇組了」）。
3. **絕對獨立檔案原則：** 每一個節點都必須是全新、獨立的 `.html` 檔案，嚴禁使用 JSON 陣列或 JavaScript 動態替換畫面。
4. **樣式沿用：** 所有新頁面的 HTML 架構與 class 必須直接對應 `style.css` 裡的設定，不可隨意更改外層 `<div>` 容器。