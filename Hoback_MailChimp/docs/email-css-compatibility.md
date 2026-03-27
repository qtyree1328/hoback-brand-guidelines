# Email HTML & CSS Compatibility Reference

What works and what doesn't across major email clients. Read this before using any CSS property you're unsure about.

---

## CSS Property Support Matrix

**Yes** = fully supported, **Partial** = works with caveats, **No** = stripped or broken.

### Layout & Box Model

| Property | Apple Mail | Gmail Web | Gmail Mobile | Outlook Desktop (Word) | New Outlook | Yahoo | Samsung |
|---|---|---|---|---|---|---|---|
| `display: block/inline/none` | Yes | Yes | Yes | Partial | Yes | Yes | Yes |
| `display: flex` | Yes | Partial | Partial | **No** | Yes | Yes | Yes |
| `display: grid` | Yes | **No** | **No** | **No** | Partial | **No** | Partial |
| `width / height` | Yes | Yes | Yes | Partial | Yes | Yes | Yes |
| `max-width` | Yes | Yes | Yes | **No** | Yes | Yes | Partial |
| `margin` | Yes | Yes | Yes | Partial | Yes | Yes | Partial |
| `padding` | Yes | Yes | Yes | Partial | Yes | Yes | Yes |
| `float` | Yes | **No** | **No** | **No** | Yes | Yes | Yes |
| `position` | Yes | **No** | **No** | **No** | **No** | **No** | **No** |

### Visual / Decorative

| Property | Apple Mail | Gmail Web | Gmail Mobile | Outlook Desktop | New Outlook | Yahoo | Samsung |
|---|---|---|---|---|---|---|---|
| `background-color` | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| `background-image` | Yes | **No** | **No** | **No** (VML) | Yes | Yes | Yes |
| `border-radius` | Yes | Yes | Yes | **No** | Yes | Yes | Yes |
| `box-shadow` | Yes | Yes | Yes | **No** | Yes | Yes | Yes |
| `linear-gradient` | Yes | **No** | **No** | **No** | Yes | Yes | Yes |
| `opacity` | Yes | Yes | Yes | **No** | Yes | Yes | Yes |
| `transform` | Yes | **No** | **No** | **No** | Partial | **No** | Partial |
| `@font-face` | Yes | **No** | **No** | **No** | Yes | **No** | Yes |

### Responsive / Media Queries

| Feature | Apple Mail | Gmail Web | Gmail Mobile | Outlook Desktop | New Outlook | Yahoo | Samsung |
|---|---|---|---|---|---|---|---|
| `@media (max-width)` | Yes | **No** | Yes | **No** | Yes | Yes | Partial |
| `@media (prefers-color-scheme)` | Yes | **No** | **No** | **No** | Partial | **No** | **No** |
| `<style>` block | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Inline styles | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| External stylesheets | Yes | **No** | **No** | **No** | **No** | **No** | **No** |

### Selectors & Pseudo-Classes

| Selector | Apple Mail | Gmail Web | Outlook Desktop | New Outlook | Yahoo | Samsung |
|---|---|---|---|---|---|---|
| `.class` | Yes | Prefixed | Yes | Yes | Yes | Yes |
| `#id` | Yes | **Stripped** | Yes | Yes | Prefixed | Replaced |
| `:hover` | Yes | Element only | **No** | Element only | Yes | Yes |
| `:checked` | Yes | **No** | **No** | **No** | Yes | Yes |
| `:nth-child` | Yes | **No** | **No** | Yes | Yes | Yes |
| Adjacent sibling (`+`) | Yes | **No** | **No** | **No** | Yes | Yes |

### Animation

| Feature | Apple Mail | Gmail | Outlook Desktop | New Outlook | Yahoo | Samsung |
|---|---|---|---|---|---|---|
| `@keyframes` | Yes | **No** | **No** | Partial | Yes | **No** |
| `transition` | Yes | **No** | **No** | Yes | Yes | Yes |

---

## Outlook Desktop Quirks (Word Rendering Engine)

Outlook 2007–2019 and 365 Classic use **Microsoft Word's HTML engine**. This is the #1 source of email rendering issues.

### What Word Does NOT Support
- `background-image` (requires VML)
- `border-radius`, `box-shadow`, `opacity`
- `flexbox`, `grid`, `float`, `position`
- `max-width`, `min-height`
- `transform`, `transition`, `animation`
- Media queries of any kind
- Any pseudo-class (`:hover`, `:checked`, etc.)
- `margin` and `padding` on `<div>` and `<img>`
- `width` and `height` on `<div>`

### MSO Conditional Comments

Target Outlook desktop only (ignored by all other clients):

```html
<!--[if mso]>
  Code ONLY for Outlook desktop
<![endif]-->

<!--[if !mso]><!-->
  Code for EVERYTHING EXCEPT Outlook desktop
<!--<![endif]-->

<!-- Specific versions -->
<!--[if mso 16]>  Outlook 2016/2019/365  <![endif]-->
<!--[if gte mso 12]>  Outlook 2007+  <![endif]-->
```

**New Outlook does NOT support MSO conditional comments** (uses Chromium).

### VML Background Images

```html
<!--[if mso]>
<v:rect xmlns:v="urn:schemas-microsoft-com:vml"
  fill="true" stroke="false" style="width:600px;height:400px;">
  <v:fill type="tile" src="https://example.com/bg.jpg" color="#333333" />
  <v:textbox inset="0,0,0,0">
<![endif]-->

<div style="background-image: url('https://example.com/bg.jpg');
            background-color: #333333; width: 600px; height: 400px;">
  Content here
</div>

<!--[if mso]>
  </v:textbox>
</v:rect>
<![endif]-->
```

### DPI Scaling Fix

Force consistent pixel rendering on high-DPI Windows displays:

```html
<!--[if gte mso 9]>
<xml>
  <o:OfficeDocumentSettings>
    <o:AllowPNG/>
    <o:PixelsPerInch>96</o:PixelsPerInch>
  </o:OfficeDocumentSettings>
</xml>
<![endif]-->
```

### Image Rules
- Always set `width` and `height` as **HTML attributes** (not just CSS)
- `max-width` is ignored — use HTML `width` attribute
- Add `display: block` to prevent phantom gap below images
- SVG not supported — use PNG

### The Dual-Outlook Transition (2025–2026)

| Version | Engine | Status |
|---|---|---|
| Outlook 2007–2019, 365 Classic | Microsoft Word | End of support: Oct 2026 |
| New Outlook for Windows | Chromium | Rolling out 2025–2026 |
| Outlook.com (web) | Browser | Current |
| Outlook iOS/Android | WebKit/Chromium | Current |

---

## Gmail Quirks

### Class & ID Handling
- **Strips all `id` attributes**
- **Renames/prefixes classes** — but `<style>` block selectors are rewritten to match, so class-based styles still work

### Style Block Gotcha
Gmail **strips the ENTIRE `<style>` block** if it finds anything it dislikes:
- Any `background-image: url(...)` rule
- Syntax errors or unrecognized at-rules
- `@font-face`, `@keyframes`, `@media (prefers-color-scheme)`

### 102KB Clipping
Gmail clips emails over ~102KB of raw HTML source. Users see a "View entire message" link most never click.
- Applies to raw HTML source, not rendered size
- Inline CSS inflates size fast — minify HTML
- **Aim for under 90KB**

### Image Proxy
- Gmail rewrites all image URLs through `ci3.googleusercontent.com/proxy/...`
- Images are cached — updated images at the same URL may show stale versions
- Use query parameters for cache-busting (`?v=2`)

### Gmail Web vs. Mobile

| Feature | Gmail Web | Gmail Mobile |
|---|---|---|
| Media queries | **No** | Yes |
| `<style>` block | Yes | Yes |
| `:hover` | Element selectors only | N/A (touch) |
| `background-image` | **No** | **No** |

---

## Dark Mode

### Client Behavior

| Client | Behavior | CSS Override |
|---|---|---|
| Apple Mail | Partial inversion; respects dev styles | Full: `color-scheme` + `prefers-color-scheme` |
| Gmail Android | Full auto-inversion | **No** |
| Gmail iOS | Minimal; follows system theme | **No** |
| Gmail Web | Mostly leaves colors alone | **No** |
| Outlook Desktop | Mostly ignores dark mode | Limited (`[data-ogsc]`) |
| New Outlook | Partial inversion | Partial (`[data-ogsc]`, `[data-ogsb]`) |
| Yahoo | Auto-inversion | **No** |
| Samsung | Respects dev styles well | Partial |

### Implementation

```html
<meta name="color-scheme" content="light dark">
<meta name="supported-color-schemes" content="light dark">

<style>
  :root { color-scheme: light dark; }

  @media (prefers-color-scheme: dark) {
    .dark-bg { background-color: #1a1a2e !important; }
    .dark-text { color: #e0e0e0 !important; }
  }
</style>
```

### Outlook Dark Mode Selectors
```css
[data-ogsc] .my-text { color: #ffffff !important; }
[data-ogsb] .my-bg { background-color: #1a1a2e !important; }
```

### Best Practices
- **Transparent PNGs disappear in dark mode.** Add background to logos or use white stroke.
- Use slightly off-white text (#e0e0e0) and off-black backgrounds (#1a1a2e)
- Always set BOTH text color AND background-color together
- Test with light and dark mode logo variants

---

## Image Handling

### Default Blocking

| Client | Blocked? |
|---|---|
| Apple Mail | No (auto-loads) |
| Gmail | No (proxied, auto-loads) |
| Outlook Desktop | **Yes (often blocked by IT policy)** |
| Yahoo | No |
| Thunderbird | **Yes (blocked by default)** |

### Format Support

| Format | Support | Notes |
|---|---|---|
| **PNG** | Universal | Safe everywhere. Logos, graphics, transparency. |
| **JPEG** | Universal | Photos. |
| **GIF (static)** | Universal | Safe. |
| **GIF (animated)** | Mostly | Outlook desktop: **first frame only** |
| **SVG** | **Not supported** | Outlook blocks. Gmail strips. Use PNG. |
| **WebP** | Unreliable | Gmail converts to JPEG. Outlook breaks. Avoid. |

### Retina / HiDPI
- Export images at **2x resolution** (1200px for a 600px display)
- Set display size via HTML `width` attribute at 1x
- `srcset` only works in Apple Mail — not a reliable solution
- Compress aggressively: JPEG quality 60–70 at 2x looks great

---

## Accessibility

### Essential Rules
- `role="presentation"` on ALL layout tables (prevents screen readers from announcing table structure)
- `lang="en"` on `<html>` (correct pronunciation)
- Every `<img>` gets `alt` attribute — decorative images use `alt=""`
- Minimum **4.5:1 contrast ratio** for body text (WCAG AA)
- Minimum **14px font size** for body text
- Link/button targets at least **44x44px** for touch
- Meaningful link text ("View our menu" not "Click here")
- Style alt text on `<img>` tags so it looks good when images are blocked:

```html
<img src="hero.jpg" alt="Spring Collection"
  width="600" height="300"
  style="display:block; width:100%; font-family:Arial,sans-serif;
         font-size:18px; color:#333; background-color:#f0f0f0;" />
```

### Semantic Elements That Work in Email
- `<h1>`–`<h6>` — use for screen reader navigation
- `<p>`, `<strong>`, `<em>`, `<ul>`, `<ol>`, `<li>` — all safe
- `<header>`, `<footer>`, `<main>` — some clients strip these, use cautiously

---

## The Safe Baseline (Works Everywhere)

### CSS That's Safe in Every Client

```css
color                    background-color
font-family              font-size
font-weight              font-style
text-align               text-decoration
line-height              letter-spacing
vertical-align           border (longhand)
border-collapse          width (on tables/TDs/images)
padding (on table cells) display: block/inline/none
```

### CSS to Avoid

```css
position    float       display: flex/grid
background-image        border-radius
box-shadow              transform
animation/transition    opacity
@font-face              max-width (Outlook)
:hover      :checked    :nth-child
```

### Safe HTML Elements

**Use freely:** `<table>`, `<tr>`, `<td>`, `<th>`, `<img>`, `<a>`, `<p>`, `<br>`, `<h1>`–`<h6>`, `<strong>`, `<em>`, `<span>`, `<div>`, `<ul>`, `<ol>`, `<li>`

**Caution:** `<style>` (in head), `<header>`, `<footer>`, `<main>`, `<button>`

**Avoid:** `<form>`, `<input>`, `<select>`, `<video>`, `<audio>`, `<svg>`, `<script>`, `<iframe>`, `<link>` (stylesheet)

### Safe Email Boilerplate

```html
<!DOCTYPE html>
<html lang="en" xmlns="http://www.w3.org/1999/xhtml"
  xmlns:v="urn:schemas-microsoft-com:vml"
  xmlns:o="urn:schemas-microsoft-com:office:office">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="color-scheme" content="light dark">
  <title>Email Subject Line</title>

  <!--[if gte mso 9]>
  <xml>
    <o:OfficeDocumentSettings>
      <o:AllowPNG/>
      <o:PixelsPerInch>96</o:PixelsPerInch>
    </o:OfficeDocumentSettings>
  </xml>
  <![endif]-->

  <style>
    body, table, td, a { -webkit-text-size-adjust: 100%; -ms-text-size-adjust: 100%; }
    table, td { mso-table-lspace: 0pt; mso-table-rspace: 0pt; }
    img { -ms-interpolation-mode: bicubic; border: 0; outline: none; text-decoration: none; }
    body { margin: 0; padding: 0; width: 100% !important; }

    @media only screen and (max-width: 620px) {
      .mobile-full { width: 100% !important; }
      .mobile-hide { display: none !important; }
      .mobile-pad { padding: 10px !important; }
    }
  </style>
</head>
<body style="margin:0; padding:0; background-color:#f4f4f4;">

  <table role="presentation" cellpadding="0" cellspacing="0" border="0"
    width="100%" style="background-color:#f4f4f4;">
    <tr>
      <td align="center">
        <table role="presentation" cellpadding="0" cellspacing="0"
          border="0" width="600" class="mobile-full"
          style="max-width:600px; background-color:#ffffff;">
          <tr>
            <td style="padding:20px; font-family:Arial, Helvetica, sans-serif;
                       font-size:16px; line-height:1.5; color:#333333;">
              <!-- Content here -->
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </table>

</body>
</html>
```

### Progressive Enhancement Strategy

1. **Baseline:** Table layout + inline styles (must work in Outlook desktop)
2. **Layer 1:** `<style>` block with class-based styles
3. **Layer 2:** Media queries for responsive (Gmail mobile, Apple Mail, Yahoo)
4. **Layer 3:** Dark mode via `prefers-color-scheme` (Apple Mail primarily)
5. **Layer 4:** Hover/transitions (Apple Mail, Yahoo)

### Rules of Thumb
- Always inline critical styles. `<style>` block is enhancement only.
- Test in: Outlook desktop, Gmail web, Gmail mobile, Apple Mail, Yahoo
- Keep HTML under **90KB** (Gmail clips at 102KB)
- Use web-safe font stacks as fallbacks
- Use `bgcolor` HTML attribute as backup for `background-color` on tables/TDs
- Include plain-text MIME alternative
