# Email Template Catalog & HTML Pattern Reference

A catalog of email types a luxury private club needs, plus the proven HTML layout patterns to build them.

---

## Part 1 — Email Template Types

### 1. Newsletter / Digest
Weekly or monthly roundup of club news, events, dining highlights, member spotlights.

**Layout:** Single-column, hero image, 2-up or 3-up card grid for features, stacked secondary items. 4–8 content sections.

**Key elements:** Branded header, hero image, section headings with dividers, thumbnail + text pairs, CTA buttons, social footer.

---

### 2. Event Invitation
Announce and drive RSVPs for dinners, galas, tournaments, mixers, seasonal openings.

**Layout:** Hero image (event photo), event details block (date/time/dress code/location), description, prominent RSVP button.

**Key elements:** Compelling event imagery, clear date/time/location, dress code, "RSVP Now" button, optional countdown, calendar add link.

---

### 3. Event Reminder
Sent 1–3 days before an event. Also doubles as "last chance to RSVP."

**Layout:** Compact single-column. Brief banner, event details reiterated, logistics (parking, weather), CTA.

---

### 4. RSVP Confirmation / Transactional
Triggered immediately after RSVP, reservation, booking, or payment.

**Layout:** Clean, minimal single-column. Confirmation header, details summary, "Add to Calendar" link, modification/cancellation link.

---

### 5. Welcome / Onboarding Series
Triggered for new members. 3–5 emails over first 30–90 days.

**Series:**
- **Day 0:** Welcome & confirmation — membership tier, login, "what to do first"
- **Day 3–5:** Facility tour — amenity highlights with photos (card grid)
- **Day 10–14:** Upcoming events — personalized recommendations
- **Day 21–30:** Meet the team — staff introductions (image + text side-by-side)
- **Day 60–90:** Check-in & feedback request

---

### 6. Announcement
Major club news: new restaurant, pool season, course renovation, policy changes.

**Layout:** Hero image, description, key details (dates/hours/pricing), photo gallery, CTA.

---

### 7. Holiday / Seasonal Greeting
Builds emotional connection. Not conversion-driven.

**Layout:** Image-heavy, minimal text. Large hero or animated GIF, brief message from leadership. Soft optional CTA.

---

### 8. Survey / Feedback Request
Post-event, seasonal satisfaction, strategic planning.

**Layout:** Clean, focused. Brief context, single CTA to survey, time estimate.

---

### 9. Re-engagement / Win-back
For members inactive 30–60–90 days. Also lapsed members near renewal.

**Layout:** "We miss you" hero, highlights of what they've missed, 2–3 upcoming events, booking CTA.

---

### 10. Menu / Schedule
Weekly dining menu, activities calendar, golf schedule, fitness classes.

**Layout:** Structured and scannable. Date/category headers, two-column (date left, details right), reservation CTAs per item.

---

### 11. Photo Recap / Gallery
Post-event recap, seasonal highlights, tournament results.

**Layout:** Hero image, 2-up or 3-up image grid, brief captions. "View Full Gallery" CTA.

---

### 12. Member Update / Account Notification
Dues statement, payment confirmation, renewal reminder, profile update, guest pass.

**Layout:** Minimal, utility-focused single-column. Clear header, structured data, action CTA.

---

## Part 2 — HTML Layout Patterns

All patterns use table-based layouts with the hybrid/spongy technique for cross-client compatibility.

### 2.1 Single-Column Layout

```html
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0"
       bgcolor="#f5f3ef" style="background-color:#f5f3ef;">
  <tr>
    <td align="center" style="padding:20px 10px;">
      <table role="presentation" width="600" cellpadding="0" cellspacing="0" border="0"
             style="max-width:600px; width:100%;" class="email-container">

        <!-- HEADER -->
        <tr>
          <td align="center" style="padding:20px 40px; background-color:#ffffff;">
            <img src="logo.png" width="180" alt="Logo"
                 style="display:block; width:180px; max-width:100%; height:auto;">
          </td>
        </tr>

        <!-- HERO IMAGE -->
        <tr>
          <td style="background-color:#ffffff;">
            <img src="hero.jpg" width="600" alt="Hero"
                 style="display:block; width:100%; height:auto;">
          </td>
        </tr>

        <!-- TEXT BLOCK -->
        <tr>
          <td style="padding:40px; background-color:#ffffff;
                     font-family:Georgia,serif; font-size:16px;
                     line-height:1.6; color:#333333;">
            <h1 style="margin:0 0 16px; font-size:24px;">Headline</h1>
            <p style="margin:0 0 16px;">Body text here.</p>
          </td>
        </tr>

        <!-- CTA -->
        <tr>
          <td align="center" style="padding:0 40px 40px; background-color:#ffffff;">
            <table role="presentation" cellpadding="0" cellspacing="0" border="0">
              <tr>
                <td bgcolor="#6b4c3b" style="background-color:#6b4c3b;">
                  <a href="#" target="_blank"
                     style="display:inline-block; padding:14px 32px;
                            font-family:Georgia,serif; font-size:15px;
                            color:#ffffff; text-decoration:none;">
                    Learn More
                  </a>
                </td>
              </tr>
            </table>
          </td>
        </tr>

      </table>
    </td>
  </tr>
</table>
```

---

### 2.2 Two-Column Side by Side (with MSO Ghost Table)

Columns stack on mobile without media queries via `inline-block` + `max-width`.

```html
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
  <tr>
    <td align="center" style="padding:20px 10px;">

      <!--[if mso]>
      <table role="presentation" width="600" cellpadding="0" cellspacing="0" border="0">
      <tr><td width="290" valign="top">
      <![endif]-->

      <div style="display:inline-block; width:100%; max-width:290px; vertical-align:top;">
        <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
          <tr>
            <td style="padding:10px; font-family:Georgia,serif; font-size:15px;
                       color:#333;">
              <h2 style="margin:0 0 10px; font-size:20px;">Column One</h2>
              <p style="margin:0;">Left column content.</p>
            </td>
          </tr>
        </table>
      </div>

      <!--[if mso]>
      </td><td width="20"></td><td width="290" valign="top">
      <![endif]-->

      <div style="display:inline-block; width:100%; max-width:290px; vertical-align:top;">
        <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
          <tr>
            <td style="padding:10px; font-family:Georgia,serif; font-size:15px;
                       color:#333;">
              <h2 style="margin:0 0 10px; font-size:20px;">Column Two</h2>
              <p style="margin:0;">Right column content.</p>
            </td>
          </tr>
        </table>
      </div>

      <!--[if mso]>
      </td></tr></table>
      <![endif]-->

    </td>
  </tr>
</table>
```

---

### 2.3 Hero Image with Text Overlay (VML for Outlook)

```html
<!--[if gte mso 9]>
<v:rect xmlns:v="urn:schemas-microsoft-com:vml" fill="true" stroke="false"
        style="width:600px; height:350px;">
  <v:fill type="frame" src="https://example.com/hero-bg.jpg" color="#3d2b1f" />
  <v:textbox inset="0,0,0,0">
<![endif]-->

<div style="max-width:600px; margin:0 auto;">
  <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0"
         style="background-image:url('https://example.com/hero-bg.jpg');
                background-color:#3d2b1f; background-size:cover;
                background-position:center;">
    <tr>
      <td align="center" style="padding:60px 40px; color:#ffffff;
                                 font-family:Georgia,serif;">
        <h1 style="margin:0 0 12px; font-size:32px; font-weight:normal;
                   color:#ffffff;">An Exclusive Evening</h1>
        <p style="margin:0 0 24px; font-size:16px; color:#f0ede8;">
          Join us for a five-course wine dinner under the stars.
        </p>
      </td>
    </tr>
  </table>
</div>

<!--[if gte mso 9]>
  </v:textbox>
</v:rect>
<![endif]-->
```

---

### 2.4 Card Grid (2-Up)

Same hybrid technique, narrower max-widths. Use `font-size:0` on parent to eliminate inline-block gaps.

```html
<!--[if mso]>
<table role="presentation" width="600" cellpadding="0" cellspacing="0" border="0">
<tr><td width="290" valign="top">
<![endif]-->

<div style="display:inline-block; width:100%; max-width:290px; vertical-align:top;">
  <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
    <tr><td style="padding:10px;">
      <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0"
             style="border:1px solid #e0dcd5;">
        <tr><td>
          <img src="card1.jpg" width="270" alt="Card" style="display:block; width:100%; height:auto;">
        </td></tr>
        <tr><td style="padding:16px; font-family:Georgia,serif; font-size:14px; color:#333;">
          <h3 style="margin:0 0 8px; font-size:17px;">Event Title</h3>
          <p style="margin:0 0 12px;">Date and details</p>
          <a href="#" style="color:#6b4c3b; font-weight:bold;">RSVP &rarr;</a>
        </td></tr>
      </table>
    </td></tr>
  </table>
</div>

<!--[if mso]>
</td><td width="20"></td><td width="290" valign="top">
<![endif]-->

<!-- Card 2: same structure -->

<!--[if mso]>
</td></tr></table>
<![endif]-->
```

**3-Up:** Use `max-width:186px` per card. Ghost table columns: 186px + 21px gutter each.

---

### 2.5 Image + Text Side by Side

Asymmetric columns (240px image / 340px text).

```html
<!--[if mso]>
<table role="presentation" width="600" cellpadding="0" cellspacing="0" border="0">
<tr><td width="240" valign="top">
<![endif]-->

<div style="display:inline-block; width:100%; max-width:240px; vertical-align:top;">
  <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
    <tr><td style="padding:10px;">
      <img src="photo.jpg" width="220" alt="Photo"
           style="display:block; width:100%; height:auto;">
    </td></tr>
  </table>
</div>

<!--[if mso]>
</td><td width="20"></td><td width="340" valign="top">
<![endif]-->

<div style="display:inline-block; width:100%; max-width:340px; vertical-align:top;">
  <table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
    <tr><td style="padding:10px; font-family:Georgia,serif; font-size:15px; color:#333;">
      <h3 style="margin:0 0 8px; font-size:18px;">Title</h3>
      <p style="margin:0 0 12px;">Description text.</p>
      <a href="#" style="color:#6b4c3b; font-weight:bold;">Read more &rarr;</a>
    </td></tr>
  </table>
</div>

<!--[if mso]>
</td></tr></table>
<![endif]-->
```

---

### 2.6 Full-Bleed Background Color Sections

Background extends edge-to-edge, content stays at 600px. Use BOTH `bgcolor` attribute AND `style="background-color"` for max compatibility.

```html
<!-- Accent section -->
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0"
       bgcolor="#3d2b1f" style="background-color:#3d2b1f;">
  <tr>
    <td align="center" style="padding:0 10px;">
      <table role="presentation" width="600" cellpadding="0" cellspacing="0" border="0"
             style="max-width:600px; width:100%;">
        <tr>
          <td style="padding:40px; font-family:Georgia,serif; font-size:16px;
                     color:#f0ede8; text-align:center;">
            <h2 style="margin:0 0 12px; font-size:22px; color:#c9a96e;
                       text-transform:uppercase; letter-spacing:1px;">
              This Season at the Club
            </h2>
            <p style="margin:0; color:#ddd8d0;">Spring is our finest season.</p>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table>
```

---

### 2.7 Countdown Timer

**Recommended: Server-generated animated GIF** (Sendtric, CountdownMail, NiftyImages). Recalculates on every open.

```html
<td align="center" style="padding:20px;">
  <img src="https://gen.sendtric.com/countdown/YOUR_ID"
       width="500" alt="Time remaining"
       style="display:block; width:100%; max-width:500px; height:auto;">
</td>
```

**Static fallback** (set at send time):

```html
<table role="presentation" cellpadding="0" cellspacing="0" border="0">
  <tr>
    <td align="center" style="padding:0 12px;">
      <div style="font-family:Georgia,serif; font-size:36px; color:#c9a96e;">03</div>
      <div style="font-family:Arial,sans-serif; font-size:11px; color:#f0ede8;
                  text-transform:uppercase; letter-spacing:1px;">Days</div>
    </td>
    <td style="font-size:28px; color:#c9a96e; padding:0 4px;">:</td>
    <td align="center" style="padding:0 12px;">
      <div style="font-family:Georgia,serif; font-size:36px; color:#c9a96e;">14</div>
      <div style="font-family:Arial,sans-serif; font-size:11px; color:#f0ede8;
                  text-transform:uppercase; letter-spacing:1px;">Hours</div>
    </td>
    <td style="font-size:28px; color:#c9a96e; padding:0 4px;">:</td>
    <td align="center" style="padding:0 12px;">
      <div style="font-family:Georgia,serif; font-size:36px; color:#c9a96e;">22</div>
      <div style="font-family:Arial,sans-serif; font-size:11px; color:#f0ede8;
                  text-transform:uppercase; letter-spacing:1px;">Min</div>
    </td>
  </tr>
</table>
```

---

### 2.8 Social Media Icon Row

Use images, not icon fonts. 32px or 40px squares with explicit dimensions.

```html
<table role="presentation" cellpadding="0" cellspacing="0" border="0">
  <tr>
    <td style="padding:0 8px;">
      <a href="https://instagram.com/yourclub"><img src="icon-instagram.png"
        width="32" height="32" alt="Instagram" style="display:block; border:0;"></a>
    </td>
    <td style="padding:0 8px;">
      <a href="https://facebook.com/yourclub"><img src="icon-facebook.png"
        width="32" height="32" alt="Facebook" style="display:block; border:0;"></a>
    </td>
  </tr>
</table>
```

---

### 2.9 Divider Patterns

**Horizontal rule:**
```html
<td style="padding:20px 40px;">
  <div style="border-top:1px solid #d4cfc7; height:1px; line-height:1px; font-size:1px;">&nbsp;</div>
</td>
```

**Spacer:**
```html
<td style="height:30px; line-height:30px; font-size:1px;">&nbsp;</td>
```

**Decorative accent:**
```html
<td align="center" style="padding:24px 0;">
  <div style="width:60px; border-top:3px solid #c9a96e; height:1px; line-height:1px; font-size:1px;">&nbsp;</div>
</td>
```

Always include `line-height`, `height`, and `font-size:1px` — prevents Outlook from collapsing or expanding empty cells. The `&nbsp;` prevents some clients from collapsing empty cells entirely.

---

## Part 3 — Structural Best Practices

### 3.1 Ghost Table Pattern for Outlook

Outlook desktop doesn't support `inline-block`, `max-width`, `flex`, or `grid`. Ghost tables inside MSO conditional comments provide a fixed-width fallback.

```html
<!--[if mso]>
<table role="presentation" width="600" cellpadding="0" cellspacing="0" border="0">
<tr><td width="300" valign="top">
<![endif]-->

<div style="display:inline-block; width:100%; max-width:300px; vertical-align:top;">
  <!-- Column content -->
</div>

<!--[if mso]>
</td><td width="300" valign="top">
<![endif]-->

<div style="display:inline-block; width:100%; max-width:300px; vertical-align:top;">
  <!-- Column content -->
</div>

<!--[if mso]>
</td></tr></table>
<![endif]-->
```

### 3.2 Hybrid / Spongy Technique

Creates responsive layouts **without media queries** — critical since Gmail web strips them.

**Principles:**
1. Use `<div>` with `display:inline-block` for columns
2. Set `width:100%` (fills narrow viewports = stacking)
3. Set `max-width:Npx` (constrains at desktop = side-by-side)
4. Wrap in ghost tables for Outlook
5. Add `@media` queries as progressive enhancement

**Why it works everywhere:**
- **Gmail:** Strips `<style>` and media queries, but `inline-block` + `max-width` work via inline styles
- **Outlook:** Ignores `inline-block`/`max-width`, but renders ghost tables
- **Apple Mail/iOS:** Full CSS support; media queries enhance further

### 3.3 Progressive Enhancement Layers

1. **Baseline (all clients):** Table layout, inline styles, system fonts, `bgcolor`
2. **Inline CSS enhancements:** `border-radius`, `max-width`, `inline-block`, CSS `background-image`
3. **Embedded `<style>`:** Hover effects, `@media` queries, `prefers-color-scheme` dark mode
4. **Interactive (nice-to-have):** CSS carousels, accordion panels — Apple Mail + few others only

### 3.4 Preheader Text Pattern

```html
<div style="display:none; font-size:1px; color:#f5f3ef; line-height:1px;
            max-height:0px; max-width:0px; opacity:0; overflow:hidden; mso-hide:all;">
  Your preview text here (40-130 chars, complements subject line).
</div>
<!-- Spacer pushes body text out of preview area -->
<div style="display:none; font-size:1px; color:#f5f3ef; line-height:1px;
            max-height:0px; max-width:0px; opacity:0; overflow:hidden;">
  &nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;
  &nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;
</div>
```

### 3.5 Bulletproof Buttons

**Method A: Padding-based (simple, no VML)**
```html
<table role="presentation" cellpadding="0" cellspacing="0" border="0">
  <tr>
    <td bgcolor="#6b4c3b" style="background-color:#6b4c3b;">
      <a href="#" style="display:inline-block; padding:14px 36px;
                         font-family:Georgia,serif; font-size:15px;
                         color:#ffffff; text-decoration:none;">
        Reserve Now
      </a>
    </td>
  </tr>
</table>
```

**Method B: VML for Outlook (bulletproof everywhere)**
```html
<!--[if mso]>
<v:roundrect xmlns:v="urn:schemas-microsoft-com:vml"
             xmlns:w="urn:schemas-microsoft-com:office:word"
             href="https://example.com"
             style="height:46px; v-text-anchor:middle; width:220px;"
             arcsize="10%" strokecolor="#6b4c3b" fillcolor="#6b4c3b">
  <w:anchorlock/>
  <center style="color:#ffffff; font-family:Georgia,serif; font-size:15px;">
    Reserve Now
  </center>
</v:roundrect>
<![endif]-->

<!--[if !mso]><!-->
<a href="https://example.com" target="_blank"
   style="display:inline-block; padding:14px 36px;
          background-color:#6b4c3b; font-family:Georgia,serif;
          font-size:15px; color:#ffffff; text-decoration:none;
          mso-hide:all;">
  Reserve Now
</a>
<!--<![endif]-->
```

**Method C: Border-based (Outlook-friendly, no VML)**
Uses thick borders on `<a>` to simulate padding. Outlook respects borders on anchors.
```html
<a href="#" style="display:inline-block; background-color:#6b4c3b;
                   color:#ffffff; font-family:Georgia,serif; font-size:15px;
                   text-decoration:none; padding:14px 36px;
                   mso-padding-alt:0;
                   border-top:14px solid #6b4c3b;
                   border-bottom:14px solid #6b4c3b;
                   border-left:36px solid #6b4c3b;
                   border-right:36px solid #6b4c3b;">
  Reserve Now
</a>
```

---

## Quick Reference: Email Type → Layout Mapping

| Email Type | Primary Layout | Key Patterns |
|-----------|---------------|-------------|
| Newsletter / Digest | Single-column + card grid | Hero, 2-up cards, image+text, dividers, social |
| Event Invitation | Single-column, hero-focused | Hero overlay (VML bg), bulletproof button, countdown |
| Event Reminder | Compact single-column | Small banner, details block, button |
| RSVP Confirmation | Minimal single-column | Data table, button, spacers |
| Welcome Series | Single-column (varies) | Hero, image+text, card grid, button |
| Announcement | Hero + single-column | Hero overlay, full-bleed sections, card grid |
| Holiday Greeting | Image-heavy single-column | Hero, full-bleed bg, minimal text |
| Survey / Feedback | Focused single-column | Short text, single CTA button |
| Re-engagement | Single-column, warm imagery | Hero, 2-up cards, button |
| Menu / Schedule | Structured 1- or 2-column | Two-column, dividers, spacers |
| Photo Recap | Image grid | 2-up/3-up cards, hero, social footer |
| Member Update | Minimal single-column | Data block, button, dividers |
