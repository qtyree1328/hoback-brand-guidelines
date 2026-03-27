# Hoback Club — Mailchimp Email Templates

This repo is the home for creating Mailchimp email templates for the Hoback Club. All templates are hand-coded (no Mailchimp drag-and-drop builder) and use Mailchimp's template language (`mc:edit`) for editable regions.

## How to Use This Repo

When asked to create a new email template:
1. Read **this file** for Hoback brand rules (colors, typography, buttons, layout)
2. Read **docs/email-template-patterns.md** for the right template type and layout patterns
3. Read **docs/email-css-compatibility.md** for what CSS works in which clients
4. Read **docs/mailchimp-template-language.md** for mc:edit, merge tags, and Mailchimp quirks
5. Read **docs/mailchimp-campaign-workflows.md** for operational context (testing, compliance, etc.)
6. Use **templates/dining-events.html** as a structural reference for the Hoback brand implementation

## Repo Structure

```
├── CLAUDE.md                          ← This file (brand rules + project guide)
├── templates/                         ← Production Mailchimp templates (paste into Mailchimp)
│   └── dining-events.html             ← First template: monthly dining events newsletter
├── docs/                              ← Reference documentation
│   ├── mailchimp-template-language.md ← mc:edit, mc:repeatable, merge tags, CSS inliner, upload methods
│   ├── email-css-compatibility.md     ← CSS support matrix, Outlook/Gmail quirks, dark mode, accessibility
│   ├── email-template-patterns.md     ← Template type catalog, HTML layout patterns with code snippets
│   ├── mailchimp-campaign-workflows.md← Campaign types, audience, testing, deliverability, compliance
│   ├── design-guide.html              ← Visual brand reference (open in browser)
│   └── setup-guide.html               ← Step-by-step Mailchimp import guide
└── assets/                            ← Source art files (NOT used in templates — use CDN URLs below)
    ├── hoback_drawing.png
    ├── tetons_drawing.png
    ├── logo-footer.svg
    └── logo-nav.svg
```

## Brand Identity for Emails

The email design mirrors the Hoback Club website — luxury private club in Jackson Hole, WY. The tone is refined, understated, and alpine. Think: high-end resort newsletter, not a promotional blast.

### Colors

| Name | Hex | Usage |
|------|-----|-------|
| Dark Blue | `#1e2d3a` | Header bar, footer, date badges, primary buttons, headings |
| Warm Tan | `#ede9e1` | Section backgrounds (intro, closing), secondary/tan buttons |
| Light BG | `#f7f5f2` | Outer wrapper, spacers between content blocks |
| White | `#ffffff` | Event card backgrounds |
| Body Text | `#272f36` | Rarely used in email — prefer #666 secondary |
| Secondary Text | `#666666` | Event descriptions, body paragraphs |
| Muted | `#999999` | Time labels, captions, legal text |
| Accent Gray | `#7a8d98` | Subheadings like "The Great Hall", time text under titles |
| Divider | `#e8e4df` | Horizontal rules, borders |
| Button Hover | `#365e75` | Hover state (CSS only, not reliable in email) |

### Typography

**Headlines:** Cormorant Garamond, weight 300 (light), always. Never bold headlines.
- Hero/intro: 32px
- Event titles: 28px
- Section headings (e.g., closing CTA): 26px
- Fallback: `Georgia, 'Times New Roman', serif`

**Body/UI:** Lato, weights 300/400/700
- Body text: 14px, weight 300, color #666, line-height 1.7
- Detail line (price/time/guests): 13px, weight 700, color #1e2d3a
- Time under title: 16px, weight 400, color #7a8d98, letter-spacing 1px
- Button text: 11px, weight 700, uppercase, letter-spacing 3px
- Labels/meta: 11px, weight 700, uppercase, letter-spacing 3px, color #999
- Legal footer: 10px, color #999
- Fallback: `Helvetica, Arial, sans-serif`

**Google Fonts link (include in `<head>`):**
```html
<link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700&family=Cormorant+Garamond:wght@300;400&display=swap" rel="stylesheet">
```

Google Fonts render in Apple Mail, iOS Mail, Gmail app. Outlook falls back to Georgia/Helvetica. This is expected and fine.

### Buttons

Five variants. ALL buttons in email must use the bulletproof table pattern — never rely on `<a>` styling alone.

| Variant | Background | Text Color | Border | Use Case |
|---------|-----------|------------|--------|----------|
| **Primary** | `#1e2d3a` | `#ffffff` | None | "View Full Menu", main CTAs on light backgrounds |
| **Tan** | `#ede9e1` | `#1e2d3a` | None | "Reserve Your Seat" on white event cards |
| **Outline** | Transparent | `#1e2d3a` | `2px solid #1e2d3a` | Tertiary actions on light backgrounds |
| **White Outline** | Transparent | `#ffffff` | `2px solid #ffffff` | CTAs on dark/image backgrounds |
| **White Solid** | `#ffffff` | `#1e2d3a` | None | High-emphasis CTA on dark backgrounds |

Shared button properties: Lato 11px/700, uppercase, letter-spacing 3px, padding 12px 32px, no border-radius (square).

**Bulletproof button pattern (use this every time):**
```html
<table role="presentation" cellspacing="0" cellpadding="0" border="0">
  <tr>
    <td style="background-color: #ede9e1; padding: 12px 32px;">
      <a href="#" style="font-family: 'Lato', Helvetica, Arial, sans-serif; font-size: 11px; font-weight: 700; color: #1e2d3a; text-decoration: none; text-transform: uppercase; letter-spacing: 3px; display: inline-block;">Button Text</a>
    </td>
  </tr>
</table>
```

### Date Badge

Square badge showing day number + month abbreviation. Used next to event titles.
- Size: 66x66px (52x52 on mobile)
- Background: `#1e2d3a`
- Day number: Cormorant Garamond 300, 26px, white
- Month: Lato 700, 10px, `rgba(255,255,255,0.6)`, uppercase, letter-spacing 2px

### Decorative Drawings

Two hand-drawn illustrations used as subtle watermarks:
- **Mountains (Teton Range):** Used in intro/hero sections at **15% opacity** (`opacity: 0.15`)
- **Building (Hoback clubhouse):** Used in closing section at **25% opacity** (`opacity: 0.25`)

These should always be very faint — they're background texture, not focal content. Never increase opacity above 25%.

## Layout Architecture

### Email Structure

```
600px container (max-width, centered)
├── Header bar (#1e2d3a, centered logo, 30px padding)
├── Intro section (#ede9e1, mountain drawing watermark, headline overlay)
├── Event cards (x3, white background)
│   ├── Title row (event name + time left, date badge right)
│   ├── Full-width image (260px height, 4px border-radius)
│   └── Description + detail line + tan CTA button
├── Spacers (16px #f7f5f2 between each card)
├── Closing section (#ede9e1, two-column table)
│   ├── Left: headline + concierge text + primary button
│   └── Right: building drawing (220px, 25% opacity)
└── Legal line (inline with closing, small unsubscribe/address text)
```

### No Footer Block

We deliberately removed the dark blue footer. The closing section (tan background with "Questions or Special Requests?") serves as the visual end of the email. The legal/unsubscribe line sits beneath it on the same tan background in small text. Do not add a separate footer section back.

### Spacing Rules

| Element | Value |
|---------|-------|
| Email max-width | 600px |
| Side padding (desktop) | 40px |
| Side padding (mobile) | 20px |
| Event card top/bottom padding | 35px |
| Between events (spacer) | 16px |
| Image height (desktop) | 260px |
| Image height (mobile) | 180px |
| Image border-radius | 4px |
| Recommended upload size | 1200x600px (2x retina) |

## HTML / CSS Rules

### Table-Based Layout Only

Email templates MUST use `<table>` for all layout. No flexbox, no CSS grid, no div positioning. Outlook renders with Word's HTML engine — only tables work reliably.

Use `role="presentation"` on all layout tables. Use `cellspacing="0" cellpadding="0" border="0"` on every table.

### Two-Column Layouts

For side-by-side content (title + date badge, closing text + drawing), use this pattern:
1. Inline-block `<div>` elements with percentage widths for modern clients
2. Wrap in `<!--[if mso]>` conditional table for Outlook
3. Add named classes for mobile media query to force `display: block !important; width: 100% !important`

### CSS Inlining

Mailchimp's CSS inliner should be **left ON** (checked). It converts `<style>` block rules to inline styles at send time. The `@media` queries are preserved (not inlined). Most styles in our templates are already inline, so the inliner is a safety net.

### Mobile Responsive

Breakpoint: `max-width: 620px`

Mobile behavior:
- Side padding reduces to 20px (`.mobile-padding`)
- Title + date badge columns stack vertically (`.event-title-col`, `.event-date-col`)
- Date badge aligns left, shrinks to 52px
- Closing section columns stack (`.closing-text-col`, `.closing-drawing-col`)
- Building drawing centers below text
- Event images reduce to 180px height
- Intro heading scales to 26px

Every multi-column section needs named classes for the media query. Inline styles alone cannot create responsive behavior — the `!important` overrides in the `@media` block are required.

### Images

- Always include `width` attribute and `alt` text on `<img>` tags
- Use `style="display: block;"` on images to prevent phantom spacing
- Mailchimp strips `width`/`height` from images that have `mc:edit` directly on the `<img>` tag — put `mc:edit` on the parent `<td>` instead
- SVG may not render in Outlook desktop. Use PNG for logos when Outlook compatibility matters (our shield logo is PNG for this reason)
- Drawings use inline `opacity` for transparency — this works in all modern clients but Outlook ignores it (drawing will appear at full opacity in Outlook, which is acceptable)

## Mailchimp-Specific

### mc:edit Regions

Every editable content block gets `mc:edit="unique_name"` on its `<td>`. This makes it clickable in Mailchimp's visual campaign editor. Rules:
- Every `mc:edit` value must be unique across the entire template
- Do NOT nest `mc:edit` inside another `mc:edit`
- Put `mc:edit` on the `<td>`, not on `<img>` or `<a>` tags (prevents Mailchimp from stripping attributes)

### Required Merge Tags

These MUST be present or Mailchimp will reject the template or auto-append an ugly footer:
- `*|UNSUB|*` — Unsubscribe link (CAN-SPAM required)
- `*|LIST:ADDRESSLINE|*` — Physical mailing address (CAN-SPAM required)

Recommended:
- `*|UPDATE_PROFILE|*` — Email preference update link
- `*|CURRENT_YEAR|*` — Auto-fills year in copyright
- `*|FNAME|*` — First name personalization

### Preview Text

Hidden preheader text that shows in inbox list views. Always include this right after `<body>`:
```html
<div style="display: none; max-height: 0; overflow: hidden; mso-hide: all;">
  Your preview text here.
  &zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp; <!-- padding to push other content out of preview -->
</div>
```

### Template Size

- Keep HTML under 102KB total — Gmail clips emails larger than this
- Mailchimp's hard limit is 200KB

## Mailchimp Content Studio URLs

All images are hosted on Mailchimp's CDN. Use these URLs directly:

```
Shield Logo (PNG):
https://mcusercontent.com/c4b9546b92e82ffccc39aa16c/images/1128138d-9212-2ebf-c730-5ca629b99ea9.png

Logo Nav (SVG):
https://mcusercontent.com/c4b9546b92e82ffccc39aa16c/files/3808e980-a573-8512-355b-384fd67f773c/logo_nav.svg

Mountains Drawing (PNG):
https://mcusercontent.com/c4b9546b92e82ffccc39aa16c/images/3014529e-7a5a-646a-3a9c-32e89256771c.png

Building Drawing (PNG):
https://mcusercontent.com/c4b9546b92e82ffccc39aa16c/images/e1d7d626-3731-d70e-5fb3-8f73f62cb84f.png
```

Do not use local file paths (`logo-footer.svg`, etc.) in templates — those won't resolve in sent emails. Always use the `mcusercontent.com` URLs above.

## Reference Documentation

For detailed Mailchimp and email HTML knowledge, see the docs/ folder:

| Document | Contents |
|----------|----------|
| `docs/mailchimp-template-language.md` | mc:edit, mc:repeatable, mc:variant, mc:hideable, mc:label, all merge tags (conditional included), CSS inliner behavior, upload methods, size limits, auto-modifications |
| `docs/email-css-compatibility.md` | CSS support matrix by client, Outlook Word engine quirks, MSO conditionals, VML, Gmail quirks (102KB clipping, style stripping), dark mode implementation, image format support, accessibility rules, safe baseline CSS |
| `docs/email-template-patterns.md` | 12 email template types (newsletter, event invite, reminder, RSVP, welcome series, announcement, holiday, survey, re-engagement, menu/schedule, photo recap, member update), HTML layout patterns with code (single-column, two-column, hero overlay, card grid, image+text, full-bleed, countdown, social icons, dividers, bulletproof buttons) |
| `docs/mailchimp-campaign-workflows.md` | Campaign types (regular, automated, A/B, RSS, transactional), template management, audience/segmentation (tags vs groups), merge fields, campaign creation workflow, testing/QA checklist, deliverability (SPF/DKIM/DMARC), analytics/UTM, CAN-SPAM/GDPR compliance |

## Design Decisions and Rationale

- **No dark blue footer:** The closing section (tan, "Questions or Special Requests?") is the visual endpoint. Legal text is minimal, same background. Adding a heavy footer made the email feel too long.
- **Tan buttons for "Reserve Your Seat":** On white event cards, the tan button is softer than dark blue. Dark blue is reserved for the primary CTA ("View Full Menu") in the closing section.
- **Time shown in two places:** Under the event title (16px, prominent) AND in the detail line with price/guests. Redundancy is intentional — the title-area time catches the eye while scanning, the detail line provides the full info block.
- **Date badge on right:** Keeps the event name as the dominant left-anchored element. The badge is a visual anchor, not primary information. On mobile it drops below the title and aligns left.
- **Mountain drawing at 15% opacity:** Higher opacity competed with the headline text overlay. 15% keeps it as subtle texture. The building drawing is slightly more visible at 25% because it sits beside text, not behind it.
- **No decorative drawings between events:** Early versions had drawings as separators. Removed — the 16px tan spacer is cleaner and the drawings added clutter.
- **Removed "The Great Hall" subheading:** Simplified the intro to just "Upcoming Dining Events" over the mountain drawing. Less text in the hero = more impact.
- **Hard-coded closing table:** The closing section (text left, building right) uses a real `<table>` with `<td>` columns, not inline-block divs. Inline-block broke in Mailchimp's renderer. Tables are bulletproof.
- **PNG logo over SVG:** Outlook desktop doesn't render SVG. The shield logo uses a PNG uploaded to Content Studio to guarantee rendering everywhere.

## Common Pitfalls

- **Don't add `mc:edit` to `<img>` tags** — Mailchimp strips width/height, breaking the layout. Put it on the parent `<td>`.
- **Don't use `<div>` for layout** — Only for inline-block column hacks with MSO conditional fallbacks.
- **Don't remove merge tags** — `*|UNSUB|*` and `*|LIST:ADDRESSLINE|*` are legally required. Mailchimp will reject or auto-append an ugly footer.
- **Don't use CSS shorthand for padding in email** — Some clients parse it wrong. Prefer `padding: 12px 32px;` (2-value is OK) but avoid 3-value or mixing with margin shorthand on the same element.
- **Don't forget `!important` in media queries** — Inline styles always win over `<style>` block rules. The only way to override them responsively is `!important` in `@media`.
- **Don't link external stylesheets** — `<link rel="stylesheet">` for non-Google-Fonts CSS is stripped by most email clients.
- **Test in actual email clients** — Mailchimp's preview is not authoritative. Send test emails to Gmail, Apple Mail, and Outlook.
