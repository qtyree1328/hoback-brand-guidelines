# Mailchimp HTML Template Language — Complete Reference

This is the authoritative reference for Mailchimp's template-specific HTML features. Read this before building any template.

---

## mc:edit — Editable Regions

The core attribute. Marks elements as editable in the Campaign Builder.

### Syntax
```html
mc:edit="unique_name"
```

The value must be **unique across the entire template**. No two regions can share the same name.

### Content Type Is Element-Dependent

Mailchimp auto-detects the editor type based on the HTML element:

**Rich Text Editor** — on container elements (`<div>`, `<td>`, `<th>`, `<p>`):
```html
<td mc:edit="body_content">
  <h2>Default headline</h2>
  <p>Default body text goes here.</p>
</td>
```

**Image Editor** — on `<img>` elements:
```html
<img mc:edit="header_image" src="placeholder.jpg" alt="Header" width="600" />
```
Gives users controls to replace, resize, add alt text, and link the image. No text editing.

**Image with Text Fallback** — using `mc:allowtext`:
```html
<img mc:edit="header_image" mc:allowtext mc:allowdesigner src="placeholder.jpg" />
```

### Nesting Rules

**CRITICAL: mc:edit regions CANNOT be nested inside other mc:edit regions.**

```html
<!-- WRONG — nested mc:edit -->
<td mc:edit="outer">
  <img mc:edit="inner_image" src="photo.jpg" />
</td>

<!-- CORRECT — sibling mc:edit regions -->
<td mc:edit="text_area"><p>Editable text</p></td>
<td mc:edit="image_area"><img src="photo.jpg" /></td>
```

### mc:edit on `<img>` — Known Pitfall

When `mc:edit` is on an `<img>` tag, Mailchimp **strips hardcoded width and height attributes** when the user edits it. This breaks retina sizing. **Workaround:** put `mc:edit` on the parent `<td>` instead (changes editor to rich text mode).

---

## mc:repeatable — Repeatable Sections

Lets users duplicate, delete, and reorder content blocks in the Campaign Builder.

### Syntax
```html
<table mc:repeatable="section_name">
  <tr>
    <td mc:edit="content_1">Default content</td>
  </tr>
</table>
```

### Behavior
- User can duplicate the block (copy below), delete it, or reorder (move up/down)
- When duplicated, Mailchimp replicates the **original coded default content**, NOT user edits
- Multiple elements can share the same `mc:repeatable` name (this enables variants)
- Do NOT place `mc:hideable` on the same element as `mc:repeatable`
- Should contain at least one `mc:edit` region inside

---

## mc:variant — Template Variants

Provides a dropdown in the Campaign Builder to switch between layout options.

### Syntax
```html
mc:variant="Descriptive Label"
```

**Must be used with `mc:repeatable`.** Multiple elements with the same `mc:repeatable` name but different `mc:variant` names are grouped. Only one variant shows at a time.

### Rules
- Variant blocks **must be adjacent siblings** (no elements between them)
- Must NOT be nested inside each other
- Each needs its own unique `mc:edit` regions

### Example
```html
<!-- Variant 1: Image Left, Text Right -->
<table mc:repeatable="product" mc:variant="Image Left">
  <tr>
    <td mc:edit="v1_image"><img src="placeholder.jpg" width="260" /></td>
    <td mc:edit="v1_text"><h4>Product Name</h4><p>Description</p></td>
  </tr>
</table>

<!-- Variant 2: Full Width Image Above Text -->
<table mc:repeatable="product" mc:variant="Stacked">
  <tr><td mc:edit="v2_image"><img src="placeholder.jpg" width="600" /></td></tr>
  <tr><td mc:edit="v2_text"><h4>Product Name</h4><p>Description</p></td></tr>
</table>
```

---

## mc:label — Section Labels

Provides a friendly name in the Campaign Builder UI.

```html
<td mc:edit="hero_txt" mc:label="Hero Section Text">
  <h1>Welcome!</h1>
</td>
```

Without it, Mailchimp displays the `mc:edit` value as the section name.

---

## mc:hideable — Hideable Sections

Adds a show/hide toggle. When hidden, the element is completely removed from sent email.

```html
<table mc:hideable>
  <tr>
    <td mc:edit="optional_banner">
      <img src="sale-banner.jpg" width="600" alt="Sale" />
    </td>
  </tr>
</table>
```

- Boolean attribute (no value)
- Do NOT combine with `mc:repeatable` on the same element
- Works on any HTML element

---

## Merge Tags — Complete Reference

Syntax: `*|TAG_NAME|*` (case-sensitive)

### Contact Field Tags

| Tag | Description |
|-----|-------------|
| `*|FNAME|*` | First name |
| `*|LNAME|*` | Last name |
| `*|EMAIL|*` | Email address |
| `*|ADDRESS|*` | Mailing address |
| `*|PHONE|*` | Phone number |

### Campaign & System Tags

| Tag | Description |
|-----|-------------|
| `*|MC_PREVIEW_TEXT|*` | Preview text (auto-generates hide CSS) |
| `*|ARCHIVE|*` | "View in browser" URL |
| `*|FORWARD|*` | Forward-to-a-friend URL |
| `*|UPDATE_PROFILE|*` | Update preferences URL |
| `*|UNSUB|*` | Unsubscribe URL **(REQUIRED)** |
| `*|LIST:NAME|*` | Audience name |
| `*|LIST:COMPANY|*` | Company name |
| `*|LIST:ADDRESS_HTML|*` | Physical address (HTML) |
| `*|LIST:ADDRESSLINE|*` | Physical address (plain text) **(REQUIRED)** |
| `*|LIST:DESCRIPTION|*` | Permission reminder |
| `*|CURRENT_YEAR|*` | Four-digit year |
| `*|DATE:FORMAT|*` | Current date (e.g., `*|DATE:d/m/Y|*`) |
| `*|CAMPAIGN_UID|*` | Unique campaign ID |

### Conditional Merge Tags

**Basic IF/ELSE:**
```html
*|IF:FNAME|*
  Hello *|FNAME|*!
*|ELSE:|*
  Hello valued member!
*|END:IF|*
```

**Comparison operators:** `=`, `!=`, `>`, `<`, `>=`, `<=`

**ELSEIF chaining:**
```html
*|IF:TRANSACTIONS >= 20|*
  <p>Gold tier benefits</p>
*|ELSEIF:TRANSACTIONS >= 10|*
  <p>Silver tier benefits</p>
*|ELSE:|*
  <p>Standard benefits</p>
*|END:IF|*
```

**IFNOT (inverse):**
```html
*|IFNOT:FNAME|*
  <p>Update your profile to personalize your experience.</p>
*|END:IF|*
```

**Group/Interest-based:**
```html
*|INTERESTED:GroupCategory:GroupName|*
  <p>Content for this interest group.</p>
*|END:INTERESTED|*
```

### Conditional Merge Tag Limitations
- AND/OR operators NOT supported in a single IF
- Do NOT work in subject lines
- Do NOT populate in test emails (only on actual sends)

---

## CSS Inliner Behavior

When enabled (Settings > Automatic CSS Inliner), Mailchimp converts `<style>` block rules to inline `style=""` attributes at **send time**.

### What gets inlined
- All CSS rules in `<style>` blocks that are NOT inside `@media` queries

### What stays in `<style>` (preserved)
- `@media` queries — left in the `<head>` for responsive clients

### Known issues
- Max size for inlining: **256KB**
- Strips quotation characters from CSS attribute selectors:
  ```css
  /* Your code */   a[href^="tel:"] { color: blue; }
  /* After inliner */ a[href^=tel:] { color: blue; }
  ```

### Best practice
```html
<style type="text/css">
  /* These get inlined */
  .body-content { font-family: Arial, sans-serif; font-size: 14px; }

  /* These are preserved for responsive clients */
  @media only screen and (max-width: 480px) {
    .body-content { font-size: 16px !important; }
  }
</style>
```

---

## Template Upload Methods

### 1. Paste HTML Code
Campaigns > Email templates > Create Template > Code your own > Paste in code

### 2. Upload ZIP File
- ZIP must be **< 1MB**
- Must contain **exactly 1 HTML file**
- All images in the **root directory** (no subfolders)
- File names: letters, numbers, hyphens only
- Mailchimp uploads images to Content Studio and rewrites paths

### 3. Marketing API
```
POST /3.0/templates
{
  "name": "My Custom Template",
  "html": "<!DOCTYPE html>...full HTML..."
}
```

Other endpoints: `GET /3.0/templates`, `PATCH /3.0/templates/{id}`, `DELETE /3.0/templates/{id}`

**Plan requirement:** Custom HTML templates require **Standard plan or higher**.

---

## Size Limits & Constraints

| Constraint | Limit |
|-----------|-------|
| Gmail clipping threshold | **102KB** (keep under this) |
| Ideal email body size | **~75KB** |
| Mailchimp hard limit | **200KB** |
| CSS inliner max | **256KB** |
| ZIP upload size | **< 1MB** |
| HTML files per ZIP | **1** |
| Image file size (recommended) | **< 1MB each** |
| Template width | **600px** |
| Image formats | **JPG, PNG, GIF** only |
| Encoding | **UTF-8** required |
| mc:edit names | Must be unique |

---

## Mailchimp's Auto-Modifications

Things Mailchimp does to your HTML that **cannot be disabled**:

### Tracking Pixel
Inserts a 1x1 transparent image at the bottom for open tracking.

### Link Wrapping
All `<a href>` links are rewritten to pass through Mailchimp's redirect servers for click tracking.

### Image Attribute Stripping
When a user edits an image via Campaign Builder, `width` and `height` attributes are stripped from `<img>` tags with `mc:edit`.

### CSS Selector Modification
Quotation characters stripped from attribute selectors (see CSS Inliner section).

### Footer Auto-Append
If `*|UNSUB|*` is missing, Mailchimp either rejects the template or auto-appends an ugly default footer.

### Preview Text Injection
`*|MC_PREVIEW_TEXT|*` becomes hidden HTML with special CSS to display in inbox previews but hide in the email body.

---

## Required Elements Checklist

Every marketing email template MUST include:

- [ ] `*|UNSUB|*` — Unsubscribe link (CAN-SPAM / Mailchimp requirement)
- [ ] `*|LIST:ADDRESSLINE|*` — Physical mailing address (CAN-SPAM requirement)
- [ ] UTF-8 charset meta tag
- [ ] `role="presentation"` on all layout tables
- [ ] Absolute URLs for all images (no relative paths)
- [ ] Preview text (either manual `<div>` or `*|MC_PREVIEW_TEXT|*`)

Recommended:
- [ ] `*|UPDATE_PROFILE|*` — Preference update link
- [ ] `*|CURRENT_YEAR|*` — Auto year in copyright
- [ ] `*|ARCHIVE|*` — "View in browser" link
