# Change Notes — site-seo-refresh

## 網域遷移實測記錄（2026-07-19）

前置條件確認：使用者已於 change 建立後自行完成 ticsee.app 註冊、DNS 設定，並直接在 main 推送兩個 commit（d4055cf Create CNAME、ca28955 chore: migrate site URLs to ticsee.app）。任務 5.1 的 CNAME 與絕對網址切換因此由使用者完成，本 session 驗證如下。

- 全站絕對網址掃描（index.html、privacy.html、sitemap.xml、robots.txt、site.webmanifest）：github.io 出現次數 = 0 ✓
- CNAME 檔內容 = ticsee.app ✓
- 舊網址轉址實測（HEAD 等效請求）：
  - https://make-a-good-soup.github.io/ticsee-privacy/privacy.html → 301 Moved Permanently → Location: http://ticsee.app/privacy.html
  - http://ticsee.app/privacy.html → 強制轉向 https://ticsee.app/privacy.html（瀏覽器落點 origin = https://ticsee.app，Enforce HTTPS 已生效）
  - 轉址鏈終點 = https://ticsee.app/privacy.html ✓（中繼多一個 http 跳點，為 GitHub Pages 實作行為，301 鏈可正常傳遞 SEO 訊號）
- HTTPS 憑證：實測初期 https://ticsee.app 曾回應 github.io 萬用憑證（TLS 錯誤），約數十分鐘後憑證核發完成，https://ticsee.app/privacy.html 已可正常以 HTTPS 取得內容 ✓
- spec 調整：seo-foundation「Legacy URL redirect verification」的 THEN 由「Location 直接為 https」修正為「301 轉址鏈終點為 https://ticsee.app/privacy.html（允許 GitHub Pages 的 http 中繼跳點）」，以符合平台實際行為。

## 使用者手動清單（design.md Migration Plan 第 5–7 步）

- [ ] Play Console：隱私權政策網址更新為 https://ticsee.app/privacy.html
- [ ] App 下一版：內建隱私權政策連結改為 https://ticsee.app/privacy.html
- [ ] Google Search Console：新增 ticsee.app 資源並提交 https://ticsee.app/sitemap.xml

## Implementation Contract 走查勾選

（2026-07-19，本地 python3 http.server + headless Chrome 全頁截圖；截圖檔存於 session scratchpad）

- [x] 隱私頁：4 張摘要卡於文件順序先於任何章節標題（1280px 與行動版截圖確認）
- [x] 隱私頁：條文恰為 6 節；內文 1637 → 1062 字（-35.1%，達 -35% 門檻）
- [x] 隱私頁：Play 揭露七項（資料類型／用途／備份分享／權限／保留刪除／兒童／聯絡）全數對應到節
- [x] 隱私頁：≤900px 顯示橫向章節導覽；點擊「保留與刪除」實測 location.hash=#retention 且頁面捲動
- [x] 隱私頁：全文無 onboarding 字串
- [x] 行銷頁：三步驟區（01–03 編號卡）與 FAQ 區（7 題摺疊卡）齊備且渲染正常
- [x] 行銷頁：FAQPage JSON-LD 與可見題目 7↔7 一對一；MobileApplication JSON-LD 解析有效
- [x] 行銷頁：可見文案關鍵詞——倒數日×2、紀念日×4、生日提醒×1
- [x] 行銷頁：3 個 play.google.com 錨點皆含 utm_source=ticsee-site／utm_medium=web／utm_campaign=landing；JSON-LD 無 utm
- [x] 行銷頁：hero 與圖庫四張截圖來源互異
- [x] 排印：標題 letter-spacing -0.015em、h1 行高 1.05、全檔無 font-weight>900；1280px 截圖「隱私權政策」無字形貼擠
- [x] 效能：assets/screens 共 204KB（<500KB）；HTML 僅 app-icon.png 與 ticsee-feature.png 為 .png 引用
- [x] 網域：絕對網址 host 全為 ticsee.app；舊網址 301 鏈終點 https://ticsee.app/privacy.html
- [x] W3C Nu validator（API 實測）：index.html errors=0、warnings=0；privacy.html errors=0（僅 2 筆 info 級 heading 建議）。附帶修正三處 div 上 aria-label 缺 role 的問題（其中兩處為改版前既有）。

補充記錄：headless Chrome 有 500px 最小視窗寬，--window-size=375 時版面以 500px 排版、截圖硬裁 375px，會產生「假裁切」；實際 375px 視口（Browser 面板實測）排版正常。走查過程中順手為 .policy-layout 行動版軌道加上 minmax(0, 1fr) 與 .policy-nav min-width: 0 作為 chip 列 min-content 傳播的防禦（無行為變化）。

## 上線後修正（2026-07-19）

使用者回報首頁 LIFE CALENDAR／YOUR NEXT MOMENT／MADE TO SHARE 圖片跑版。以 820／1000／1280／500 四寬度重現，確認四個病灶並修正：

1. MADE TO SHARE 標題在 ≥950px 爆行出現孤字（字距放寬的迴歸）→ 標題比照全站慣例加 br 斷行。
2. phone-stage 絕對定位裁切在中間寬度留空或貼頂 → 改 object-fit: cover + object-position: center top，素材完整填滿舞台。
3. TIME FLOW／YOUR NEXT MOMENT 在 680–900px 堆疊時 min-height 560 造成大面積空洞 → 該區間改 min-height: 0 + padding-bottom 保留底部裝飾空間。
4. card-screen（widgets 圖）在 >680px 貼死卡片頂邊 → 改頂部錨定 top: clamp(170px, 18vw, 230px)，680px 以下維持原底部錨定。

驗證：四寬度 headless 全頁截圖通過；教訓——初版走查漏掉 680–1280 中間寬度帶。

## 響應式圖片第二輪修正（2026-07-19）

使用者再次回報一頁式首頁圖片全面跑版。實際瀏覽器量測確認，第一輪修正只處理了中寬版空洞，沒有建立共用圖片比例契約：

- 1280px 圖庫圖片被排成 380×1280（正確 9:16 應約 380×676）；375px 則為 285×1280（正確應約 285×507）。根因是全域 img 只有 max-width: 100%，HTML height 屬性仍固定為 1280，縮寬後高度沒有同步。
- life-calendar.webp 是完整 9:16 行銷素材，但 phone-stage 以橫向容器搭配 object-fit: cover，素材標題與手機畫面在不同寬度被裁掉。
- widgets 圖同樣因固定 1280px 高度與絕對定位疊加，導致 desktop／mobile 的裁切位置不可預測。

修正策略：全域圖片採 height: auto；gallery 與 widgets 的 image box 明確維持 9:16；hero 與 life-calendar 使用 contain 保留完整構圖；widgets 只在橘色 feature card 內做可控的垂直 crop。行動圖庫保留下一張 peek，新增滑動提示、scroll snap、overscroll containment 與鍵盤 focus ring。

驗證矩陣（in-app browser 實測）：

| viewport | document overflow | gallery 比例 | widgets 比例 | hero / life fit | 最小 CTA 高度 |
| --- | ---: | ---: | ---: | --- | ---: |
| 360 | 0 | 0.5625 | 0.5625 | contain / contain | 44px |
| 390 | 0 | 0.5625 | 0.5625 | contain / contain | 44px |
| 768 | 0 | 0.5625 | 0.5625 | contain / contain | 44px |
| 1024 | 0 | 0.5625 | 0.5625 | contain / contain | 44px |
| 1280 | 0 | 0.5625 | 0.5625 | contain / contain | 44px |
| 1440 | 0 | 0.5625 | 0.5625 | contain / contain | 44px |

共用 styles 回歸檢查：privacy.html 於 375／1280px document overflow 均為 0；行動章節導覽仍為可橫向捲動 chip 列，四張摘要卡維持 2×2。

## 核心內容可見性第三輪修正（2026-07-19）

使用者以實際頁面截圖指出：比例數值雖已正確，Life Calendar 日曆格與 widgets 核心內容仍遭 wrapper 裁切，桌面 MADE TO SHARE 圖過大，TIME FLOW 也未忠於 Ticsee V2。這次不再只驗 `width / height = 0.5625`，而增加「來源上下界完整可見」與「核心功能內容進入畫面」兩個驗收層次。

- Life Calendar：移除固定 660px 舞台與 absolute image，圖片以 max-width 420px／height auto 決定容器高度；680px 以下先顯示產品圖再顯示 52 週說明卡，375px 首屏即可看到日曆格。
- TIME FLOW：讀取 V2 `TimeFlowSection.kt`、`TimeFlowProgressRing.kt` 與 `ProgressRing.kt`，按原始 token 與 -210° 起點／240° sweep／round cap 幾何，以三張 1:1 inline-SVG 卡重建。
- ON YOUR HOME SCREEN：由絕對定位＋負 bottom 改為兩欄（行動版單欄）grid，完整 9:16 商店素材自然撐高卡片，四種 widget 均保留。
- MADE TO SHARE：桌面三張圖各上限 320px，height auto；900px 以下切換 snap rail，避免平板硬擠與桌面海報化。

in-app browser 實測 1280×900 與 375×812：四區皆無非等比拉伸；桌面與行動 TIME FLOW 皆維持三卡單列；日曆格與四種 widget 可見；行動圖庫可見下一張 peek。第三輪修正未改動 privacy.html，後續以共用 CSS overflow 與 W3C 驗證補做最終回歸。
