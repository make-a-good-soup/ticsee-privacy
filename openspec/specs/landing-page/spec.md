# landing-page Specification

## Purpose

TBD - created by archiving change 'site-seo-refresh'. Update Purpose after archive.

## Requirements

### Requirement: FAQ section with matching structured data

The landing page SHALL include an FAQ section containing at least 5 question-and-answer entries rendered with native details and summary elements. The page SHALL embed a FAQPage JSON-LD script whose Question and acceptedAnswer entries correspond one-to-one with the visible FAQ entries. The existing MobileApplication JSON-LD SHALL remain present and valid.

#### Scenario: FAQ entries and structured data stay in sync

- **WHEN** the FAQ section renders N visible entries
- **THEN** the FAQPage JSON-LD contains exactly N Question objects whose name fields equal the visible question texts

##### Example: planned question set

| Question | Keyword it carries |
| -------- | ------------------ |
| Ticsee 是什麼？ | 人生日曆、時間進度 |
| 人生日曆是什麼？ | 人生日曆、週數 |
| Ticsee 需要註冊或付費嗎？ | 免費、無廣告 |
| 我的資料會上傳到雲端嗎？ | 隱私、備份 |
| 有哪些桌面小工具？ | 桌面小工具、widget |
| 可以倒數生日、紀念日嗎？ | 倒數日、紀念日、生日提醒 |
| 支援 iOS 嗎？ | Android |

#### Scenario: FAQ works without JavaScript

- **WHEN** a visitor activates a collapsed FAQ entry with JavaScript disabled
- **THEN** the answer expands via native details element behavior


<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->

---
### Requirement: Three-step getting-started section

The landing page SHALL present a getting-started section with exactly 3 ordered steps: install from Google Play, set birthday and planning horizon to generate the life calendar, add a home-screen widget and create the first countdown event. Each step SHALL be described in a single sentence.

#### Scenario: Visitor reads the onboarding path

- **WHEN** a visitor scrolls past the screenshot gallery
- **THEN** the three ordered steps are visible with step numbers and one sentence each


<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->

---
### Requirement: Long-tail keyword coverage in visible copy

The visible landing page copy SHALL contain each of the following Traditional Chinese terms at least once: 倒數日, 紀念日, 生日提醒. Poetic h1 and h2 headings SHALL remain unchanged; keyword placement SHALL live in section body copy, the FAQ, and the getting-started section.

#### Scenario: Keyword audit passes

- **WHEN** the rendered landing page text is searched for the three terms
- **THEN** each term is found at least once in visible content


<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->

---
### Requirement: Play Store links carry campaign attribution

Every anchor element linking to the Google Play listing SHALL include the query parameters utm_source=ticsee-site, utm_medium=web, and utm_campaign=landing. The downloadUrl and installUrl values inside JSON-LD SHALL remain free of UTM parameters.

#### Scenario: All Play anchors are tagged

- **WHEN** the landing page anchors pointing at play.google.com are enumerated
- **THEN** each anchor URL contains utm_source=ticsee-site and the JSON-LD URLs contain no utm parameters

##### Example: tagged Play link

- **GIVEN** the base listing URL for package net.makeagoodsoup.ticsee
- **WHEN** the header call-to-action anchor is inspected
- **THEN** its href ends with id=net.makeagoodsoup.ticsee&utm_source=ticsee-site&utm_medium=web&utm_campaign=landing


<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->

---
### Requirement: Screenshot gallery uniqueness and copy-image consistency

The screenshot gallery SHALL display three pairwise-distinct images, none of which duplicates the hero screenshot. Share-card copy SHALL match displayed evidence: the count wording SHALL be 多款 unless six distinct share-card designs are shown on the page.

#### Scenario: No duplicate screenshots

- **WHEN** the hero image and the three gallery images are compared by source file
- **THEN** all four source files are distinct


<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->

---
### Requirement: Responsive marketing media preserves source composition

The landing page SHALL preserve the 9:16 source aspect ratio of every App marketing image without non-uniform scaling. Hero, life-calendar, gallery, and widgets media SHALL render at natural height with contain-style composition; the source image's top and bottom edges SHALL NOT be clipped by a fixed-height or absolutely positioned wrapper. The life-calendar preview SHALL visibly include the calendar grid, and the widgets preview SHALL visibly include all four widget designs contained in the source asset. On desktop, each gallery image SHALL be no wider than 320 CSS pixels. At 900px and below, the gallery SHALL become a horizontally scrollable, keyboard-focusable rail with a visible swipe hint and SHALL NOT create document-level horizontal overflow.

#### Scenario: Marketing images remain undistorted across device widths

- **WHEN** the page is rendered at 360, 390, 768, 1024, 1280, and 1440 CSS pixels wide
- **THEN** gallery, life-calendar, and widgets media retain a 9:16 rendered aspect ratio with their full source bounds visible, the life-calendar grid and all four widget designs are present in the rendered image, and the document has no horizontal overflow

#### Scenario: Mobile gallery exposes more content without breaking the page

- **WHEN** a visitor views the gallery at 900 CSS pixels wide or below
- **THEN** the first 9:16 card and part of the next card are available in a snap-scrolling rail, a swipe hint is visible, and keyboard focus has a visible indicator

#### Scenario: Mobile visitors see the calendar before supporting metrics

- **WHEN** a visitor views the Life Calendar showcase at 680 CSS pixels wide or below
- **THEN** the complete 9:16 Life Calendar preview appears before the 52-weeks explanatory card in visual order, with the calendar grid visible inside the first preview


<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->

---
### Requirement: Time Flow mirrors the Ticsee V2 component

The Time Flow feature SHALL mirror the light-theme Ticsee V2 `TimeFlowSection`: three equal square cards for WEEKLY, MONTHLY, and YEARLY; orange, indigo, and emerald accents respectively; matching tinted card backgrounds; centered percentage and label; and a rounded 240-degree progress arc beginning at -210 degrees. The section SHALL remain legible as a three-card row at desktop, tablet, and mobile widths.

#### Scenario: Time Flow visual contract remains faithful across widths

- **WHEN** the page is rendered at 375, 768, and 1280 CSS pixels wide
- **THEN** the Time Flow card contains three square tinted tiles in one row, each uses a rounded 240-degree arc and the WEEKLY/MONTHLY/YEARLY labels, and none of the percentage or label text is clipped

<!-- @trace
source: site-seo-refresh
updated: 2026-07-19
code:
  - assets/screens/life-calendar.webp
  - assets/screens/home-dashboard.png
  - CNAME
  - assets/screens/widgets.png
  - assets/screens/event-countdown.png
  - assets/screens/home-dashboard.webp
  - privacy.html
  - sitemap.xml
  - styles.css
  - assets/screens/widgets.webp
  - assets/screens/share-card.png
  - assets/screens/event-countdown.webp
  - assets/screens/life-calendar.png
  - assets/screens/share-card.webp
  - robots.txt
  - index.html
-->