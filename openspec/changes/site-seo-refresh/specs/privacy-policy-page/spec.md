## ADDED Requirements

### Requirement: Layered summary precedes full policy text

The privacy policy page SHALL display a summary layer of at least 3 promise cards above the full policy body. The cards SHALL cover, at minimum: no account required, no ads and no third-party analytics, data stays on the device, and system backup is controlled by Android.

#### Scenario: Visitor sees the summary before the policy body

- **WHEN** a visitor opens privacy.html
- **THEN** the promise cards are rendered between the policy hero and the first policy section, before any section heading is visible in document order

### Requirement: Condensed six-section policy retains mandatory disclosures

The policy body SHALL consist of exactly six sections in this order: data processed and purposes, network connections and backup and sharing, system permissions, retention and deletion, security and children's privacy, policy updates and contact. Scope and developer identity statements SHALL be merged into the lead-in block. Every disclosure topic required by the Google Play User Data policy SHALL remain present. Each section SHALL contain at most 3 sentences of prose plus at most 4 bullet items, each bullet a single sentence. The Android permission list SHALL be retained with one sentence per permission. The total visible text of the policy body SHALL be at least 35% shorter than the pre-change baseline.

#### Scenario: Required disclosure topics map to sections

- **WHEN** the condensed policy is reviewed against the disclosure checklist
- **THEN** every checklist topic resolves to exactly one section

##### Example: disclosure-to-section mapping

| Disclosure topic | Section |
| ---------------- | ------- |
| Data types processed on device | Data processed and purposes |
| Purposes of processing | Data processed and purposes |
| Transfers via backup and user-initiated sharing | Network, backup and sharing |
| Android permissions used | System permissions |
| Retention and deletion paths | Retention and deletion |
| Children's privacy stance | Security and children's privacy |
| Developer contact channel | Policy updates and contact |

#### Scenario: Density budget is respected

- **WHEN** any single policy section is inspected
- **THEN** it contains at most 3 sentences of prose and at most 4 single-sentence bullets

### Requirement: Section navigation is available on narrow viewports

On viewports 900px wide or narrower, the page SHALL render a horizontally scrollable section navigation below the policy hero. Activating a navigation item SHALL scroll the page to the corresponding section anchor.

#### Scenario: Mobile visitor navigates to a section

- **WHEN** a visitor at 375px viewport width taps the retention-and-deletion item in the section navigation
- **THEN** the page scrolls to the retention-and-deletion section heading

### Requirement: Policy text uses Traditional Chinese terminology without developer jargon

The visible policy text SHALL NOT contain the English term "onboarding". App-internal notions SHALL be expressed in plain Traditional Chinese, including 初次設定進度 for first-run state and 已發送提醒的紀錄 for the notification dedup record.

#### Scenario: Jargon-free policy body

- **WHEN** the rendered policy body text is searched for the string "onboarding"
- **THEN** zero matches are found
