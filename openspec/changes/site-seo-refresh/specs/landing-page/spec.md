## ADDED Requirements

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

### Requirement: Three-step getting-started section

The landing page SHALL present a getting-started section with exactly 3 ordered steps: install from Google Play, set birthday and planning horizon to generate the life calendar, add a home-screen widget and create the first countdown event. Each step SHALL be described in a single sentence.

#### Scenario: Visitor reads the onboarding path

- **WHEN** a visitor scrolls past the screenshot gallery
- **THEN** the three ordered steps are visible with step numbers and one sentence each

### Requirement: Long-tail keyword coverage in visible copy

The visible landing page copy SHALL contain each of the following Traditional Chinese terms at least once: 倒數日, 紀念日, 生日提醒. Poetic h1 and h2 headings SHALL remain unchanged; keyword placement SHALL live in section body copy, the FAQ, and the getting-started section.

#### Scenario: Keyword audit passes

- **WHEN** the rendered landing page text is searched for the three terms
- **THEN** each term is found at least once in visible content

### Requirement: Play Store links carry campaign attribution

Every anchor element linking to the Google Play listing SHALL include the query parameters utm_source=ticsee-site, utm_medium=web, and utm_campaign=landing. The downloadUrl and installUrl values inside JSON-LD SHALL remain free of UTM parameters.

#### Scenario: All Play anchors are tagged

- **WHEN** the landing page anchors pointing at play.google.com are enumerated
- **THEN** each anchor URL contains utm_source=ticsee-site and the JSON-LD URLs contain no utm parameters

##### Example: tagged Play link

- **GIVEN** the base listing URL for package net.makeagoodsoup.ticsee
- **WHEN** the header call-to-action anchor is inspected
- **THEN** its href ends with id=net.makeagoodsoup.ticsee&utm_source=ticsee-site&utm_medium=web&utm_campaign=landing

### Requirement: Screenshot gallery uniqueness and copy-image consistency

The screenshot gallery SHALL display three pairwise-distinct images, none of which duplicates the hero screenshot. Share-card copy SHALL match displayed evidence: the count wording SHALL be 多款 unless six distinct share-card designs are shown on the page.

#### Scenario: No duplicate screenshots

- **WHEN** the hero image and the three gallery images are compared by source file
- **THEN** all four source files are distinct
