## Why

Ticsee 官網（GitHub Pages）兩頁已完成視覺改版，但仍有四個阻礙 SEO 與轉換的問題：(1) 隱私權政策頁條文先行、缺乏摘要層，訪客第一眼感受複雜；(2) 行銷頁缺少 FAQ 與上手引導等能承載長尾搜尋詞的內容，實質文字量偏薄；(3) 中文標題套用拉丁負字距造成字形貼擠，且五張截圖 PNG 共約 1.3MB 拖累 LCP；(4) 產品首頁網址 make-a-good-soup.github.io/ticsee-privacy/ 以 "privacy" 路徑與 github.io 子網域承載品牌，是搜尋信任與點閱率的結構性劣勢，而 ticsee.app 經註冊局 RDAP 查證目前未註冊。為配合 SEO 推廣時程，一次完成內容分層、SEO 擴充、排印修正與網域遷移準備。

## What Changes

- 隱私權政策頁改為分層式：頂部新增 30 秒摘要卡（3–4 張承諾卡）；條文由 8 節併為 6 節；句子密度向 2025-06-28 舊版靠攏，但保留現行揭露範圍（Google Play User Data 政策底線，不刪合規內容）；行動版恢復章節導覽（現為 display none）；「onboarding 狀態」等英文夾雜用語中文化。
- 行銷頁新增「常見問題」區（5–7 題，含 FAQPage JSON-LD）與「三步驟上手」區；「倒數日」「紀念日」「生日提醒」等同義搜尋詞自然置入文案；三處 Google Play 連結加上 UTM 參數；圖庫抽換與 hero 重複的截圖；「六款分享卡片」文案與實際展示對齊。
- 全站中文排印修正：大標題字距與行高調整為中文安全值、字重統一 900；slogan 層級統一（主句「讓時間，被你看見。」用於 og 與 footer，輔句「看見時間，也記得好好生活。」用於 lede 與結尾 CTA）；清除 policy-nav 無效的計數器 CSS。
- 五張 App 截圖由 PNG 轉為 WebP，改善載入效能。
- 網域遷移準備：新增 CNAME 檔、全站絕對網址（canonical、OG、JSON-LD、sitemap、robots）切換為 https://ticsee.app/、github.io 舊網址 301 轉址實測步驟，以及 Play Console 政策網址與 App 內建連結的更新清單。前置條件：使用者完成 ticsee.app 註冊與 DNS 設定後，網域相關任務才可執行。

## Capabilities

### New Capabilities

- `landing-page`: 產品一頁式行銷頁的內容結構與 SEO 要求（FAQ 區、三步驟上手區、結構化資料、UTM、圖文一致性）
- `privacy-policy-page`: 分層式隱私權政策頁（摘要層、條文密度、合規揭露底線、行動版章節導覽）
- `seo-foundation`: 全站 SEO 基礎（自訂網域與轉址、meta 與結構化資料一致性、圖片效能、中文排印規範）

### Modified Capabilities

(無 — openspec/specs 目前為空，全部為新增)

## Impact

- Affected specs: 新增 landing-page、privacy-policy-page、seo-foundation 三個 capability
- Affected code:
  - Modified: index.html, privacy.html, styles.css, sitemap.xml, robots.txt
  - New: CNAME, assets/screens/home-dashboard.webp, assets/screens/life-calendar.webp, assets/screens/widgets.webp, assets/screens/share-card.webp, assets/screens/event-countdown.webp
  - Removed: assets/screens/home-dashboard.png, assets/screens/life-calendar.png, assets/screens/widgets.png, assets/screens/share-card.png, assets/screens/event-countdown.png
- 外部系統（使用者手動操作，非本 change 產出）：ticsee.app 網域註冊與 DNS 設定、GitHub Pages 自訂網域綁定、Play Console 隱私權政策網址更新、App 下一版內建連結更新、Google Search Console 資源新增
