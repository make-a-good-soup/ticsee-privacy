## Context

Ticsee 官網託管於 GitHub Pages，僅兩個頁面（index.html 行銷頁、privacy.html 政策頁）與一份共用樣式 styles.css，無建置流程、無 JS 框架。行銷目標是讓繁中使用者以「人生日曆」「倒數日」「時間進度」等詞搜尋到 Ticsee。討論階段已確認四個問題：政策頁條文先行且行動版無目錄、行銷頁缺長尾詞內容、中文標題被拉丁負字距擠壓（已截圖確認）、網址結構（github.io 子網域＋ticsee-privacy 路徑）對品牌搜尋不利。ticsee.app 經 .app 註冊局 RDAP 查證目前未註冊；git 歷史顯示曾綁定 privacy.ticsee.app 子網域後移除。

## Goals / Non-Goals

**Goals:**

- 隱私頁 30 秒內可理解：摘要層先行，條文可掃讀，行動版有導覽
- 行銷頁承載長尾搜尋詞並提升轉換引導（FAQ、三步驟、UTM 歸因）
- 中文排印在 Android／Windows／macOS 系統字型下皆穩定可讀
- 網域遷移到 ticsee.app 的一切站內準備就緒，剩餘步驟有明確清單與順序

**Non-Goals:**

- 不做視覺 redesign：色彩、版型、卡片系統、英文 kicker 風格全部保留
- 不將 h1／h2 改寫為關鍵字標題（title 與 meta 已承載關鍵字，缺口由新增區塊補）
- 不刪除 Google Play User Data 政策要求的任何揭露項目——只縮句、合併、粗化粒度
- 不假造社會證明（評分、下載數）；待 Play 有真實數據後另案加入
- 不做英文版頁面與 hreflang
- 不含網域購買、DNS 設定、Play Console 操作、App 端修改（列入遷移清單由使用者執行）

## Decisions

### 隱私權政策分層改寫

採「新版揭露範圍 × 舊版句子密度」：保留現行八節的全部揭露項目，但重排為「摘要卡＋六節條文」。政策 hero 下方新增四張摘要卡（不需帳號／無廣告、無追蹤／資料留在你的手機／備份由 Android 系統控制）。現行「適用範圍」縮為一句併入「先說重點」導言（App 套件名 net.makeagoodsoup.ticsee、開發者 Make a Good Soup、適用本網站）；「保存在裝置上的資料」與「資料如何被使用」合併為「我們處理哪些資料、用來做什麼」，資料清單由五項逐欄位粗化為三類（個人設定與事件內容／App 與提醒設定／分享暫存圖片）。六節順序：資料與用途、連線備份與分享、系統權限、保留與刪除、安全與兒童隱私、政策更新與聯絡。密度基準：每節正文至多 3 句、bullet 至多 4 條且每條 1 句；全文較現行縮減約四成。權限清單保留三項權限卡（是信任資產）。「onboarding 狀態」改為「初次設定進度」、「傳送紀錄」改為「已發送提醒的紀錄（避免重複通知）」。行動版（900px 以下）章節導覽由隱藏改為政策 hero 下方的橫向可捲動 chip 列。替代方案「大幅刪減條文」因 Play 審核與透明度風險否決；「摺疊式 accordion」因增加互動複雜度且對縮短感受幫助有限而未採用。

### 行銷頁 SEO 區塊（FAQ 與三步驟上手）

新增兩個區塊承載關鍵字，不動既有詩意標題。「三步驟上手」置於分享卡片圖庫之後、隱私承諾之前：下載 Ticsee（Google Play）→ 設定生日與規劃年限，得到你的人生日曆 → 把小工具放上桌面、建立第一個倒數日。「常見問題」置於隱私承諾之後、結尾 CTA 之前，7 題草案：Ticsee 是什麼／人生日曆是什麼／需要註冊或付費嗎（免費、無廣告、無帳號）／資料會上傳雲端嗎（連往政策頁）／有哪些桌面小工具／可以倒數生日、紀念日嗎／支援 iOS 嗎。FAQ 以 details 元素摺疊呈現並附 FAQPage JSON-LD（獨立 script 標籤）。誠實評估：Google 已限縮 FAQ rich snippet 的顯示對象，本區塊的主要價值在長尾詞內容與轉換疑慮處理，不押注 rich snippet。同義詞「倒數日」「紀念日」「生日提醒」自然置入 FAQ 與三步驟文案。三處 Play 連結（導覽、hero、結尾 CTA）加上 utm_source=ticsee-site、utm_medium=web、utm_campaign=landing；JSON-LD 內的 downloadUrl 與 installUrl 保持乾淨網址不加 UTM。圖庫第三格抽換與 hero 重複的首頁截圖，改用桌面小工具截圖；「六款分享卡片」改為「多款分享卡片」以維持圖文一致（若使用者確認補足六張展示圖可改回）。

### 中文排印修正與 slogan 統一

大標題（兩頁 h1 與各節 h2 共用規則）字距由 -0.075em 放寬為 -0.015em，hero 與政策頁 h1 行高由 0.88 調至 1.05；全站 font-weight 950 統一為 900（Noto Sans TC 與 Inter 的實際上限，避免 faux bold 跨平台不一致）。footer 標語由「把時間變成你看得見的進度。」改為主句「讓時間，被你看見。」，與 og:title 一致；「看見時間，也記得好好生活。」維持為 lede 與結尾 CTA 的輔句。hero 下方 microcopy 增加「無廣告」成為：Android・免費下載・無廣告・不需註冊帳號。刪除 policy-nav 上無效的 counter-reset 樣式（計數器從未輸出）。替代方案「引入 Noto Sans TC webfont 統一渲染」因增加 100KB 級載入成本、與效能目標衝突而否決。

### 截圖 WebP 轉檔

五張 assets/screens 下的 PNG（合計約 1.3MB）以 cwebp 品質 82 轉為同名 WebP，HTML 引用同步改為 .webp，img 的 width／height 屬性維持 720×1280 不變；轉檔後刪除舊 PNG。app-icon.png 與 ticsee-feature.png（og:image 用）維持 PNG 以確保社群平台預覽相容。不做 srcset：素材只有單一 720px 寬版本，顯示尺寸至多約 450px，增益有限。

### 網域遷移與絕對網址切換

目標配置：apex 網域 ticsee.app 綁定 GitHub Pages（DNS 需四筆 A 記錄 185.199.108.153、185.199.109.153、185.199.110.153、185.199.111.153，www 子網域以 CNAME 指向 make-a-good-soup.github.io），儲存庫根目錄新增內容為 ticsee.app 的 CNAME 檔。全站絕對網址切換為 https://ticsee.app/：index.html 的 canonical、og:url、og:image、twitter:image、JSON-LD 的 image 與 screenshot；privacy.html 的 canonical、og:url、og:image；sitemap.xml 兩筆 loc；robots.txt 的 Sitemap 行。選 apex 而非沿用先前的 privacy 子網域：本站主體已是產品首頁，品牌搜尋應落在主網域，政策頁自然成為 ticsee.app/privacy.html。此決策整批任務有硬前置：使用者完成網域註冊與 DNS 設定前不得合併 CNAME 與網址切換（CNAME 先上而 DNS 未生效會使站點離線）。

## Implementation Contract

- 行為（隱私頁）：訪客在政策 hero 下方先看到至少 3 張摘要卡；條文為 6 節；在 375px 寬視口可見橫向章節導覽並可點擊跳至各節；policy-article 內文字數較現行版本減少 35% 以上；Play 政策要求的揭露項目（資料類型、用途、備份與分享、權限、保留刪除、兒童隱私、聯絡方式）在頁面上皆可找到對應敘述。
- 行為（行銷頁）：頁面存在三步驟上手區與 FAQ 區；FAQ 至少 5 題且附 FAQPage JSON-LD；「倒數日」「紀念日」「生日提醒」三詞各至少出現一次於可見文案；三個指向 Google Play 的 a 連結 querystring 皆含 utm_source=ticsee-site；圖庫三張截圖互不重複且不與 hero 重複。
- 介面／資料形狀：FAQPage JSON-LD 為合法 schema.org 結構（mainEntity 為 Question／acceptedAnswer 陣列）；既有 MobileApplication JSON-LD 保持有效；HTML 結構維持無 JS 依賴（details 摺疊為原生行為）。
- 排印：styles.css 中大標題規則的 letter-spacing 為 -0.015em、h1 行高 1.05，全檔無 font-weight 950；以 1280px 寬截圖目視確認政策頁 h1「隱私權政策」無字形貼擠。
- 效能：assets/screens 目錄合計小於 500KB；兩頁 HTML 中除 app-icon.png 與 ticsee-feature.png 外無 .png 引用。
- 網域（於使用者完成註冊與 DNS 後驗收）：以 curl -I 請求舊網址 https://make-a-good-soup.github.io/ticsee-privacy/privacy.html 得到 301 且 Location 為 https://ticsee.app/privacy.html；canonical、og:url、sitemap、robots 中所有絕對網址的 host 均為 ticsee.app；https://ticsee.app 以 HTTPS 正常回應兩頁。
- 驗證方式：本地以 python3 http.server 目視兩頁桌面（1280px)與行動（375px）版；FAQ JSON-LD 貼入 Google Rich Results Test 無錯誤；HTML 以 W3C validator 檢查無 error 級問題。
- 範圍邊界：本 change 只改動 index.html、privacy.html、styles.css、sitemap.xml、robots.txt、CNAME 與 assets/screens 圖檔；App 程式碼、Play Console 設定、DNS、Search Console 均為使用者手動清單項目，不在 apply 範圍。

## Risks / Trade-offs

- [GitHub 官方文件未保證 github.io 舊網址在綁定自訂網域後 301 轉址（社群實測通常會）] → 轉址列為驗收條件實測；若實測不轉址，App 既有版本的內建政策連結會失效，緩解順序：Play Console 政策網址先行更新、App 下一版更新內建連結、必要時保留一段過渡期不合併網址切換
- [CNAME 先合併而 DNS 未生效會使整站離線] → 網域相關任務標記硬前置「使用者完成註冊與 DNS」，與內容任務分批合併
- [條文縮寫過頭可能遺漏 Play 要求的揭露] → Implementation Contract 列出揭露項目對照清單作為驗收；縮句不刪項
- [WebP 直接取代 PNG 對極舊瀏覽器不相容] → WebP 自 2020 起全主流瀏覽器支援，目標受眾為 Android 使用者，風險可忽略；og:image 保持 PNG
- [FAQ rich snippet 已限縮，SEO 效益低於預期] → 區塊價值定位在長尾詞內容與轉換，不依賴 rich snippet；成本僅為靜態內容
- [ticsee.app 目前無人註冊，公開討論後存在被搶註的時間風險] → 建議使用者在實作開始前先完成註冊（費用約每年 12–20 美元）

## Migration Plan

1. [使用者] 註冊 ticsee.app 並設定 DNS（四筆 A 記錄＋www CNAME）
2. 合併內容與排印批次（不含 CNAME 與網址切換，站點行為不變）
3. 使用者確認 DNS 生效後，合併 CNAME＋絕對網址切換批次；於 GitHub Pages 設定綁定 ticsee.app 並啟用 Enforce HTTPS
4. 實測新網址與舊網址 301 轉址並記錄結果
5. [使用者] 更新 Play Console 隱私權政策網址為 https://ticsee.app/privacy.html
6. [使用者] App 下一版更新內建政策連結
7. [使用者] Google Search Console 新增 ticsee.app 資源並提交 sitemap
回滾策略：刪除 CNAME 檔並還原網址切換 commit 即回復 github.io 運作。

## Open Questions

- 分享卡片實際款數：若確認為六款且願意補足六張展示圖，「多款分享卡片」文案可改回「六款」
- FAQ 的 iOS 題答案口徑（目前規劃寫「目前僅 Android，iOS 尚未定案」）需使用者確認
- ticsee.app 註冊商由使用者自選；若最終選用其他網域名稱，網址切換清單照用、僅替換 host
