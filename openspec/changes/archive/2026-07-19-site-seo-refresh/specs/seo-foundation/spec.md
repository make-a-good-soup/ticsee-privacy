## ADDED Requirements

### Requirement: Custom domain readiness with consistent absolute URLs

The repository SHALL contain a CNAME file whose content is exactly ticsee.app. All self-referencing absolute URLs across the site SHALL use the https://ticsee.app/ origin, covering: canonical links, og:url, og:image, twitter:image, JSON-LD image and screenshot values, sitemap loc entries, and the robots.txt Sitemap line. This requirement is gated: the CNAME file and URL switch SHALL NOT be merged to the default branch before the user confirms domain registration and DNS configuration, because an active CNAME without working DNS takes the site offline.

#### Scenario: URL audit after the domain switch

- **WHEN** the domain batch is applied and both pages plus sitemap.xml and robots.txt are scanned for absolute self-referencing URLs
- **THEN** every match uses the https://ticsee.app/ origin and zero matches use the make-a-good-soup.github.io origin

#### Scenario: Legacy URL redirect verification

- **WHEN** after DNS binding the old URL https://make-a-good-soup.github.io/ticsee-privacy/privacy.html is requested with a HEAD request
- **THEN** the response status is 301 and the redirect chain terminates at https://ticsee.app/privacy.html (an intermediate http hop issued by GitHub Pages is acceptable), and the observed result is recorded in the change notes; a non-redirecting result triggers the fallback sequence defined in the design (Play Console URL first, app update next)

### Requirement: Screenshot image performance budget

All app screenshots under assets/screens SHALL be WebP files, the directory total SHALL be under 500KB, and page HTML SHALL NOT reference any .png asset except app-icon.png and ticsee-feature.png. Image elements SHALL keep explicit width and height attributes of 720 by 1280.

#### Scenario: Performance budget audit

- **WHEN** assets/screens is listed and both HTML files are scanned for .png references
- **THEN** the directory contains only .webp screenshots totalling under 500KB and the only .png references are app-icon.png and ticsee-feature.png

##### Example: converted screenshot set

| File | Format |
| ---- | ------ |
| assets/screens/home-dashboard.webp | WebP |
| assets/screens/life-calendar.webp | WebP |
| assets/screens/widgets.webp | WebP |
| assets/screens/share-card.webp | WebP |
| assets/screens/event-countdown.webp | WebP |

### Requirement: CJK-safe heading typography

Display heading rules shared by both pages SHALL use a letter-spacing of -0.015em, h1 rules SHALL use a line-height of at least 1.05, and no CSS rule SHALL declare a font-weight above 900.

#### Scenario: Stylesheet typography audit

- **WHEN** styles.css is scanned for letter-spacing, line-height, and font-weight declarations on heading rules
- **THEN** heading letter-spacing values are -0.015em or wider, h1 line-height is at least 1.05, and no font-weight exceeds 900

#### Scenario: Visual crowding check on the policy title

- **WHEN** privacy.html is rendered at 1280px viewport width and the h1 隱私權政策 is inspected in a screenshot
- **THEN** adjacent glyphs do not touch or overlap

### Requirement: Brand slogan hierarchy is consistent site-wide

The footer tagline on both pages SHALL be 讓時間，被你看見。 and the supporting line 看見時間，也記得好好生活。 SHALL appear in the hero lede and the final call-to-action of the landing page. The hero microcopy SHALL read: Android・免費下載・無廣告・不需註冊帳號. Dead navigation counter CSS on the policy table of contents SHALL be removed.

#### Scenario: Slogan audit across pages

- **WHEN** both rendered pages are searched for the two slogan lines
- **THEN** the footer of each page carries 讓時間，被你看見。 and the landing hero lede plus final call-to-action carry 看見時間，也記得好好生活。
