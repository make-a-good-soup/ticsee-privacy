## 1. 隱私權政策分層改寫

- [x] 1.1 將 privacy.html 條文重寫為六節結構、適用範圍併入導言：每節至多 3 句正文與 4 條單句 bullet、內文較現行縮減 35% 以上、design.md 揭露對照表項目全數保留（spec: Condensed six-section policy retains mandatory disclosures）。驗證：逐項核對揭露對照表，並以字數統計比對改寫前後的 policy-article 內文。
- [x] 1.2 在政策 hero 與第一節之間新增至少 3 張摘要承諾卡，訪客未捲動條文前即可讀到重點（spec: Layered summary precedes full policy text）。驗證：1280px 與 375px 截圖中，摘要卡於文件順序上先於任何章節標題出現。
- [x] 1.3 900px 以下改為顯示橫向可捲動章節導覽，點擊項目捲動至對應章節錨點（spec: Section navigation is available on narrow viewports）。驗證：375px 視口點擊「保留與刪除」導覽項，頁面捲動至該節標題。
- [x] 1.4 條文用語全面中文化，改用「初次設定進度」「已發送提醒的紀錄」等說法（spec: Policy text uses Traditional Chinese terminology without developer jargon）。驗證：對 privacy.html 全文搜尋 onboarding 字串為零筆。

## 2. 行銷頁 SEO 區塊（FAQ 與三步驟上手）

- [x] 2.1 於隱私承諾與結尾 CTA 之間新增 FAQ 區：至少 5 題、以原生 details 與 summary 呈現、並嵌入與可見題目一對一的 FAQPage JSON-LD，既有 MobileApplication JSON-LD 保持有效（spec: FAQ section with matching structured data）。驗證：將頁面原始碼貼入 Google Rich Results Test 無錯誤；停用 JavaScript 後仍可展開答案。
- [x] 2.2 於圖庫與隱私承諾之間新增三步驟上手區（下載 → 設定生日與規劃年限 → 放上小工具並建立第一個倒數日），每步一句，且全頁可見文案各出現至少一次「倒數日」「紀念日」「生日提醒」（spec: Three-step getting-started section；spec: Long-tail keyword coverage in visible copy）。驗證：渲染文字搜尋三個詞各至少一筆，三步驟含編號逐步顯示。
- [x] 2.3 三處指向 Google Play 的連結加上 utm_source=ticsee-site、utm_medium=web、utm_campaign=landing，JSON-LD 內 downloadUrl 與 installUrl 保持無 UTM（spec: Play Store links carry campaign attribution）。驗證：列舉頁面上 play.google.com 錨點逐一檢查參數，JSON-LD 內無 utm 字串。
- [x] 2.4 圖庫第三格抽換為桌面小工具截圖、分享卡片數量文案改為「多款」（spec: Screenshot gallery uniqueness and copy-image consistency）。驗證：hero 與圖庫三張圖的來源檔案四者互異。

## 3. 中文排印修正與 slogan 統一

- [x] 3.1 styles.css 標題規則調整為 letter-spacing -0.015em、h1 line-height 1.05、全檔無 font-weight 高於 900，並移除 policy-nav 無效的計數器樣式（spec: CJK-safe heading typography）。驗證：掃描 styles.css 相關宣告值符合規格，且 1280px 截圖中「隱私權政策」標題字形無貼擠。
- [x] 3.2 兩頁 footer 標語改為「讓時間，被你看見。」、hero microcopy 改為 Android・免費下載・無廣告・不需註冊帳號，輔句「看見時間，也記得好好生活。」維持於 lede 與結尾 CTA（spec: Brand slogan hierarchy is consistent site-wide）。驗證：兩頁渲染文字搜尋主句與輔句，位置與規格一致。

## 4. 截圖 WebP 轉檔

- [x] 4.1 五張 assets/screens 截圖以 cwebp 品質 82 轉為同名 WebP、HTML 引用同步改為 .webp 並保留 720×1280 寬高屬性、刪除舊 PNG（spec: Screenshot image performance budget）。驗證：assets/screens 目錄合計小於 500KB，兩頁 HTML 中除 app-icon.png 與 ticsee-feature.png 外無 .png 引用。

## 5. 網域遷移與絕對網址切換（硬前置：使用者完成 ticsee.app 註冊與 DNS 設定）

- [x] 5.1 新增內容為 ticsee.app 的 CNAME 檔，並將 index.html 與 privacy.html 的 canonical、og:url、og:image、twitter:image、JSON-LD 圖址與 sitemap.xml 的 loc、robots.txt 的 Sitemap 行全數切換為 https://ticsee.app/ 開頭；前置條件未確認前本任務不得合併（spec: Custom domain readiness with consistent absolute URLs）。驗證：全站掃描絕對網址，github.io 出現次數為零。
- [x] 5.2 網域綁定並啟用 Enforce HTTPS 後，以 HEAD 請求實測舊網址 301 轉址至 https://ticsee.app/privacy.html 並將結果記錄於 change 筆記；若未轉址，依 design.md 網域遷移與絕對網址切換一節的 fallback 順序處理，並於 PR 描述引用 design.md Migration Plan 的使用者手動清單（Play Console、App 內建連結、Search Console）（spec: Custom domain readiness with consistent absolute URLs）。驗證：curl 輸出記錄存檔且清單三項齊備。

## 6. 整體驗證

- [x] 6.1 本地以 python3 http.server 走查兩頁桌面 1280px 與行動 375px 版面（hero、摘要卡、章節導覽、FAQ、三步驟、footer），對照 design.md Implementation Contract 逐項確認。驗證：走查截圖存檔並在 change 筆記勾選對應契約條目。
- [x] 6.2 兩頁 HTML 通過 W3C validator 檢查無 error 級問題。驗證：validator 輸出無 error。

## 7. 響應式圖片與跨裝置體驗補強

- [x] 7.1 修正共用圖片 sizing contract：預設 height auto，gallery 與 widgets 圖維持 9:16，hero／life-calendar 改為 contain 構圖，移除造成非等比拉伸與意外裁切的 cover／固定高度組合（spec: Responsive marketing media preserves source composition）。驗證：360／390／768／1024／1280／1440px 六寬度量測比例與 object-fit。
- [x] 7.2 680px 以下圖庫改為保留下一張預覽的橫向 snap rail，補滑動提示、鍵盤焦點與 overscroll containment（spec: Mobile gallery exposes more content without breaking the page）。驗證：360／390px rail scrollWidth > clientWidth、頁面 document overflow = 0、最小 CTA 高度 ≥44px。
- [x] 7.3 重新走查首頁 hero、Life Calendar、feature cards、widgets、gallery、steps 與 CTA，並確認共用 styles 對 privacy.html 無回歸。驗證：首頁六寬度與政策頁 375／1280px document overflow 均為 0。

## 8. 核心內容可見性與 Ticsee V2 視覺對齊

- [x] 8.1 Life Calendar 取消固定高度裁切，讓 9:16 素材以自然高度完整呈現；680px 以下將產品圖排在 52 週說明卡之前（spec: Responsive marketing media preserves source composition）。驗證：375／1280px 截圖可見日曆格，圖片上下界未被 wrapper 截斷。
- [x] 8.2 TIME FLOW 依 Ticsee V2 `TimeFlowSection`／`ProgressRing` 重做為三張 1:1 淺色卡與 240° round-cap arcs，沿用橘／靛／綠 accent 與 WEEKLY／MONTHLY／YEARLY 標籤（spec: Time Flow mirrors the Ticsee V2 component）。驗證：375／1280px 目視比對元件排列、顏色、弧形幾何與文字無裁切。
- [x] 8.3 ON YOUR HOME SCREEN 改為文案與完整 9:16 素材的響應式 grid，不使用 absolute positioning 或負 bottom crop（spec: Responsive marketing media preserves source composition）。驗證：375／1280px 可見素材中的事件、人生進度、時間與 Time Flow 四種 widget，rendered ratio = 0.5625。
- [x] 8.4 MADE TO SHARE 桌面圖片上限 320px 並使用自然高度；900px 以下啟用橫向 rail（spec: Responsive marketing media preserves source composition）。驗證：375px 可見下一張 peek，1280px 三張等寬且無拉長，兩者皆維持 9:16。
