Prompt: 
I am preparing to provide the design company a full redesign package, with the injectable modules, design guide, and showcase.html.

I want the showcase.html to be the source document for everything. It should contain the whole brand guidelines/brand style, the component/module library, and the components

I want the core document, we will call it BrandGuidelines.html to contain this all in a very professional demonstration. 


It should start with the core brand guidelines, such as the following:
logo system
color palette
typography
imagery style
iconography
spacing / layout rules
email or marketing style examples
usage rules and examples

For the email template, just show an example email template (Hoback_MailChimp/dining-events.html) and then have a button to see all the details on another page (whats contained in Hoback_MailChimp/docs).

Then there should be an Image gallery section, which is a gallery of images that should be acceptable on the site. emphasize that this is exhaustive. the image urls are located here:
images.txt

Then it contains a section on website structure- this just lays out the list of public and private facing pages (including new ones, like Mountain).  under each page should be a brief description of what changes are going to be made

Then it contains the component library, which is like showcase.html, but needs to be more exaustive of all the components in my redesign and actually contain them all, not show text with redirection to another site. The showcase should show where each section lives (what sub page). If it makes sense, maybe the showcase is organized by page. Then, it needs to clearly show where a new page (Mountain) is and its features. Also, add a button/line that indicates the weight/size of a given module, and how easy it is to integrate

the folder that you will create needs to contain all the necessary information and files that BrandGuidelines.html uses. Make sure that this is professional and is up to the standard that website designers expect.

Claude comments (it kept crashing, so liekly incomplete):
Here's the full build plan for brand-guidelines/BrandGuidelines.html:

BrandGuidelines.html — Build Plan
Folder Structure

brand-guidelines/
├── BrandGuidelines.html    ← the master document
All images are external URLs — no local assets needed.

Document Layout
Fixed left sidebar (~240px, #1e2d3a) with nav links to each section
Scrollable main content on the right
Fonts: Lato + Cormorant Garamond (Google Fonts)
Professional, agency-quality brand book feel
Sidebar Nav Links
Logo System
Color Palette
Typography
Imagery & Gallery
Spacing & Layout
Button System
Email & Marketing
Website Structure
Component Library
Section 1: Cover / Hero
Full-width dark blue (#1e2d3a) hero
Shield logo: https://mcusercontent.com/c4b9546b92e82ffccc39aa16c/images/1128138d-9212-2ebf-c730-5ca629b99ea9.png
Title: "Hoback Club Brand Guidelines"
Subtitle: "Redesign Package — Prepared for Club Essential"
Version: March 2026
Section 2: Logo System
Show shield logo (PNG URL above) and wordmark SVG: https://mcusercontent.com/c4b9546b92e82ffccc39aa16c/files/3808e980-a573-8512-355b-384fd67f773c/logo_nav.svg
Show on dark bg AND light bg (side by side)
Clear space rule: minimum padding = logo height
Minimum size: 40px height
Do/Don't text list (don't stretch, don't recolor, don't add effects)
Section 3: Color Palette
Render swatches (colored div + hex + RGB + usage note) for:

Name	Hex	Usage
Dark Blue	#1e2d3a	Header, footer, buttons, badges
Warm Tan	#ede9e1	Section backgrounds, secondary buttons
Light BG	#f7f5f2	Page background, spacers
White	#ffffff	Content cards
Body Text	#272f36	Primary text
Secondary	#666666	Descriptions
Muted	#999999	Captions, meta
Accent Gray	#7a8d98	Subheadings
Button Hover	#365e75	Hover state
Divider	#e8e4df	Borders, rules
Live Indicator	#4ade80	Webcam live dots
Section 4: Typography
Cormorant Garamond 300 — headlines only. Sizes: 4.2rem (hero), 2.4rem (section), 1.2rem (sub-section)
Lato 300/400/700 — everything else. Sizes: 0.9rem body, 0.75rem labels (uppercase, 0.15-0.2em tracking), 0.7rem nav
Show live rendered examples of each
Include the Google Fonts <link> tag and fallback stacks
Section 5: Imagery & Gallery
Intro text: "This is the exhaustive approved image library. All website imagery should be sourced from this collection."
Photography style notes: alpine luxury, natural light, warm earth tones, Jackson Hole landscape
Image gallery grid (responsive, 4-col desktop, 3-col tablet, 2-col mobile) with click-to-enlarge (open in new tab via <a target="_blank">)
Images from images.txt (converted to direct URLs):


https://hobackclub.com/images/dynamic/getImage.gif?ID=100147
through
https://hobackclub.com/images/dynamic/getImage.gif?ID=100172
(IDs: 100147-100160, 100162-100172 — skip 100161)

Also include a note with the original CE admin URL format:
https://hobackclub.com/Default.aspx?p=.NETCEEditorPFSTC&NoNav=1&ShowFooter=Falsenoimgtrack=1&NoModResize=1&ID={ID}

Images already used on the site (from my earlier audit):


IDs: 100023, 100032, 100043, 100048, 100065, 100066, 100067, 100068, 100077, 100083, 100085, 100087, 100088, 100089, 100091, 100092, 100093, 100094, 100096, 100097, 100099, 100100, 100101, 100102, 100103, 100104, 100105, 100106, 100107, 100108, 100109, 100110, 100111, 100112, 100113, 100114, 100116, 100117, 100118, 100119, 100120, 100121, 100122, 100123, 100124, 100125, 100126, 100127, 100128, 100129, 100130, 100133, 100142, 100143
External approved images:

https://www.datocms-assets.com/50871/1680193117-skier-winter-promo-box-ajimmerson_powder_12-3-2022-1103-jpg.jpg
https://realestate.theclearcreekgroup.com/wp-content/uploads/sites/2/2016/09/Fall-Colors-Jackson-Hole-1030x579.jpg
https://www.travelandleisure.com/thmb/YiylyFMlqZz6kD-78-4g_dHdxHU=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/TAL-deck-hoback-club-wyoming-HOBACKCLUB0126-16ecbcfb0dcf4eceb5f9cb6c44323a13.jpg
https://media.assettype.com/resident%2F2025-10-08%2Fx5guk5jw%2F1911_Teton_Great_Hall_02_40.jpg?rect=1%2C0%2C2999%2C1687
https://bloximages.newyork1.vip.townnews.com/jhnewsandguide.com/content/tncms/assets/v3/editorial/1/d7/1d768df0-f5da-43da-b43d-a4c721ffbec8/5e3a42ed3329f.image.jpg
# Hoback Project Handoff

This file is the practical pickup note for the `hoback-demo` workspace.

## What This Repo Contains

There are three related work areas in this repo:

1. The main static Hoback Club demo site at the repo root.
2. Reusable HTML snippets in `injectable-modules/` for Club Essential injection.
3. Mailchimp email template work in both `mailchimp-templates/` and `Hoback_MailChimp/`.

## Current Repo Shape

### Static Site

The root contains standalone HTML pages with inline CSS/JS, including:

- `index.html`
- `mountain.html`
- `lifestyle.html`
- `dining.html`
- `discover.html`
- `stay.html`
- `amenities.html`
- `contact-us.html`
- `concierge.html`
- `membership.html`
- `member.html`
- `login.html`

There is no app build system here. This is a static HTML/CSS/JS workspace.

### Injectable Modules

`injectable-modules/` contains self-contained sections copied from the site so they can be embedded elsewhere. Each module file includes:

- a `<style>` block
- the HTML block
- any section-specific JS

`injectable-modules/_showcase.html` is the preview page for those snippets.

If a section exists both in a top-level page and in `injectable-modules/`, keep them visually aligned when editing.

### Mailchimp Work

There are two Mailchimp directories:

- `mailchimp-templates/`
- `Hoback_MailChimp/`

They currently overlap heavily. The structured, better-documented version is `Hoback_MailChimp/`, and that should be treated as the safer source of truth unless there is a reason to preserve the older folder in parallel.

For dining email work, start with:

- `Hoback_MailChimp/CLAUDE.md`
- `Hoback_MailChimp/templates/dining-events.html`

## Brand Rules

The brand is refined, understated, alpine, and luxury-club oriented. Avoid loud promotional styling.

### Core Colors

- Dark blue: `#1e2d3a`
- Warm tan: `#ede9e1`
- Light background: `#f7f5f2`
- Body text: `#272f36`
- Secondary text: `#666666`
- Accent gray: `#7a8d98`
- Divider: `#e8e4df`

### Typography

- Headings: `Cormorant Garamond`, light weight
- Body/UI: `Lato`

Across both web and email work, the visual language leans on high contrast, generous spacing, serif headlines, restrained body copy, and square-edged controls.

## Email-Specific Rules

For Mailchimp templates:

- Use table-based layout only.
- Keep `mc:edit` values unique.
- Put `mc:edit` on parent `<td>` elements, not directly on `<img>` or `<a>`.
- Preserve required merge tags such as `*|UNSUB|*` and `*|LIST:ADDRESSLINE|*`.
- Use the Mailchimp CDN asset URLs already documented in `Hoback_MailChimp/CLAUDE.md`.
- Keep the existing closing tan section; do not reintroduce a heavy separate footer.

The current dining template pattern is a 600px centered container with:

- dark blue logo header
- tan intro section with faint mountain drawing
- stacked white event cards
- tan closing CTA section with building drawing

## Working Notes

- `brand-guidelines/Readme.md` was empty when this handoff was reconstructed.
- `git status` currently shows untracked work in `Hoback_MailChimp/`, `brand-guidelines/`, `injectable-modules/`, `mailchimp-templates/`, and `images.txt`, plus a modified `.vscode/settings.json`.
- There are no obvious TODO markers in the repo indicating a single unfinished feature.
- The Mailchimp template in `mailchimp-templates/hoback-email-template.html` and `Hoback_MailChimp/templates/dining-events.html` appears materially duplicated.

## Recommended Operating Assumptions

When continuing work:

1. Treat the repo root pages as the live site mockups.
2. Treat `injectable-modules/` as extracted reusable sections that may need syncing after page edits.
3. Treat `Hoback_MailChimp/` as the canonical email-template workspace.
4. Avoid letting the two Mailchimp folders drift unless the user explicitly wants both maintained.

## First Places To Read

If picking the project up cold, read these first:

- `Hoback_MailChimp/CLAUDE.md`
- `injectable-modules/README.md`
- `index.html`
- the specific top-level page you are modifying

If the task is email-only, also read:

- `Hoback_MailChimp/docs/email-template-patterns.md`
- `Hoback_MailChimp/docs/email-css-compatibility.md`
- `Hoback_MailChimp/docs/mailchimp-template-language.md`

## Main Risks

- Editing a site section without updating its injected module equivalent.
- Editing the wrong Mailchimp folder and creating divergence.
- Breaking email compatibility by introducing modern layout CSS into templates.
- Swapping local asset paths into email HTML instead of CDN-hosted image URLs.
