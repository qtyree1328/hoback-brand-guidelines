# Mailchimp Campaign Workflows & Operations Reference

Everything about working with Mailchimp operationally — campaign types, audience management, testing, deliverability, and compliance.

---

## Campaign Types

### Regular Campaigns
The standard one-time send. Design content, pick recipients, send or schedule.
- Full control over content, subject, from address, send time
- Can be duplicated for future use as a starting point

### Automated Campaigns (Marketing Automation Flows)
Triggered by events, dates, or subscriber behavior.

**Triggers (Starting Points):**
- Subscriber joins audience
- Tag is added to contact
- Cart abandonment
- Date-based (birthday, anniversary)
- Contact doesn't open a campaign
- Churn risk changes

**Flow Points:** Delays, if/else branches, send email, add/remove tags, update fields. Supports up to 3 triggers per flow. Standard/Premium plans unlock the full journey builder with branching.

### A/B Test Campaigns
Test 2–3 variations, auto-send winner to the rest of the list.

**Testable variables:** Subject line, from name, content, send time

**Process:**
1. Define variations and the variable to test
2. Choose test group size (e.g., 20% gets A, 20% gets B)
3. Set winning metric (open rate, click rate, revenue)
4. Set wait time before picking winner
5. Winner auto-sends to remaining list

**Multivariate testing** (Premium only) tests combinations across up to 8 variations.

### RSS-Driven Campaigns
Auto-pulls from an RSS feed on a schedule. If new content exists, it sends. If not, no email.

Uses RSS merge tags: `*|RSSITEMS|*`, `*|RSSTITLE|*`, `*|RSSFULL|*`

### Transactional Email (Mandrill)
One-to-one triggered emails via API/SMTP — password resets, order confirmations, etc.
- Requires Standard or Premium plan
- Separate API key from Marketing API
- Uses Handlebars syntax for dynamic content
- Pay-per-email pricing

---

## Template Management

### Upload Methods
1. **Paste code:** Campaigns > Email templates > Create Template > Code your own
2. **Upload HTML file:** Single `.html` file
3. **Upload ZIP:** One HTML file + images in root, < 1MB, no subfolders

### Organization
Mailchimp has no folders or tags for templates. Use clear naming:
`[Brand]-[Type]-[Version]` → e.g., `Hoback-Events-v3`

### Updating vs. Creating New
- **Updating in place:** Changes apply to future campaigns. Already-sent campaigns are unaffected. Drafts in progress are NOT auto-updated.
- **Creating new versions:** Duplicate (Replicate), rename with version indicator. Safer for production.

### Version Control Best Practice
- Keep consistent `mc:edit` names across versions — Mailchimp uses these to map content when switching templates
- Maintain source HTML in this repo; paste into Mailchimp after changes
- Mailchimp has NO built-in version history

---

## Audience & Segmentation

### Audiences (Lists)
Top-level container for contacts. Most plans limit to 1–3 audiences.
- A contact in 2 audiences counts as 2 toward billing
- **Best practice:** One audience, segmented — not multiple audiences

### Tags
Admin-applied labels for internal organization.
- Applied manually, via import, automations, API, or hidden signup fields
- Invisible to subscribers
- Use to build segments (e.g., "VIP", "Event-Attendee-Mar")

### Groups
Subscriber-facing preferences (checkboxes on signup forms).
- Organized as Group Categories (question) → Group Names (options)
- Example: "Interests" → "Dining Events", "Wine Tastings", "Outdoor Activities"

**Tags vs. Groups:** Tags = admin classification. Groups = subscriber self-selection.

### Merge Fields
Data columns in your audience. Each stores one piece of data per contact.

**Default fields:** FNAME, LNAME, EMAIL, ADDRESS, PHONE

**Custom fields:** Add at Audience > Settings > Audience fields. Mailchimp assigns tags like `*|MERGE6|*` — rename to something meaningful like `*|MEMBERID|*`.

**Default values:** Set fallback for empty fields. E.g., FNAME default = "Member" so `Hello *|FNAME|*` → "Hello Member" when blank.

---

## Campaign Creation — Step by Step

### 1. Create Campaign
Campaigns > Create Campaign > Email > Regular. Name it (internal only).

### 2. Configure Recipients (To)
Select audience → Entire audience, segment, tag, or group. Personalize "To" with merge tags.

### 3. Configure From
- **From name:** What recipients see (e.g., "Hoback Club")
- **From email:** Must be verified on an authenticated domain
- **Reply-to:** Can differ from From email

### 4. Subject & Preview Text
- **Subject:** Keep under 50 chars for mobile. Can include merge tags.
- **Preview text:** 40–90 characters. If not set, clients pull first visible body text.

### 5. Design
Choose template, edit content via visual editor (mc:edit regions) or code editor.

### 6. Review
Mailchimp flags: missing subject, broken links, missing merge tags, auth warnings.

### 7. Test
Send test emails. Run Inbox Preview (Litmus). Check links.

### 8. Send or Schedule
- **Send now:** Enters queue immediately
- **Schedule:** Pick date/time
- **Send Time Optimization:** Mailchimp picks optimal time per subscriber (Standard+)
- **Timewarp:** Same local time across time zones (Premium only)

---

## Testing & QA

### Built-in Preview
Desktop/mobile toggle in campaign editor. Visual approximation only — NOT how it renders in real clients.

### Inbox Preview (Litmus)
Screenshots from dozens of real clients. 25 tokens/month on paid plans. Takes 1–3 min. Essential for catching Outlook, dark mode, and mobile issues.

### Link Checker
Preview > Check email links. Flags broken URLs and empty hrefs.

### Send Test Email
1. Preview and Test > Send a Test Email
2. Up to 12 addresses
3. Subject prefixed with "Test:"
4. Merge tags render with YOUR data or defaults, not per-recipient
5. Does NOT count toward send quota

### QA Checklist (Every Send)
- [ ] Test to Gmail, Apple Mail/iOS, and Outlook
- [ ] All links correct and working
- [ ] Images load (check alt text with images disabled)
- [ ] Merge tags render correctly (especially FNAME defaults)
- [ ] Preview text displays as intended
- [ ] Mobile rendering verified
- [ ] Subject line — no typos, good length
- [ ] From name and email correct
- [ ] Run link checker
- [ ] Run Inbox Preview if tokens available

---

## Deliverability

### Email Authentication (Required)

**SPF:** DNS TXT record listing authorized sending servers. Must include Mailchimp's servers.

**DKIM:** 2 CNAME records pointing to Mailchimp's key servers. Without it, Gmail shows "via mailchimpapp.net."

**DMARC:** DNS TXT record telling receivers what to do with failing emails. Required by Gmail/Yahoo for 5,000+ daily senders.
- Minimum: `v=DMARC1; p=none;`
- Recommended: `v=DMARC1; p=quarantine; rua=mailto:dmarc-reports@yourdomain.com;`

**Setup:** Account > Domains > Add & verify. Mailchimp provides the DNS records. Add them at your registrar.

### Avoiding Spam Filters

**Authentication:** SPF + DKIM + DMARC (non-negotiable)

**List hygiene:**
- Only email opt-in contacts
- Remove inactive subscribers (no engagement in 6–12 months)
- Use double opt-in
- Never purchase lists
- Clean bounces (Mailchimp handles hard bounces automatically)

**Content:**
- Avoid trigger words ("FREE!!!", "Act Now", excessive caps)
- Maintain text-to-image ratio (don't go all-images)
- Don't use link shorteners (bit.ly etc. — flagged by filters)
- Keep under 102KB to avoid Gmail clipping

**Engagement:**
- Encourage replies (signals legitimacy)
- High open/click rates improve sender reputation
- Segment and target — relevance drives engagement

### From Address Best Practices
- Use a real, monitored address (never "noreply@")
- Use your own domain (never gmail.com/yahoo.com)
- Keep consistent — switching confuses filters
- Authenticate the domain

### Subject Line Best Practices
- 50 characters or fewer
- Front-load important info
- Personalize with merge tags when relevant
- Max 1 emoji
- Avoid ALL CAPS and excessive punctuation
- A/B test regularly

---

## Analytics & Tracking

### Open Tracking
1x1 pixel fires when images load. **Apple Mail Privacy Protection (iOS 15+)** pre-fetches all images, inflating open rates. Mailchimp flags "MPP opens" separately. Click rate is now the more reliable engagement metric.

### Click Tracking
All links rewritten through Mailchimp's tracking servers. Reports show total clicks, unique clicks, per-link click maps. Can be disabled per campaign.

### UTM Parameters
| Parameter | Typical Value |
|-----------|--------------|
| `utm_source` | `mailchimp` |
| `utm_medium` | `email` |
| `utm_campaign` | `mar-2026-events` |
| `utm_content` | `hero-cta` (optional) |

### Google Analytics Integration
Enable in Settings > Tracking > "Google Analytics link tracking." Mailchimp auto-appends utm_source, utm_medium, utm_campaign. **Do NOT also add manual UTMs** — creates duplicates.

---

## Compliance

### CAN-SPAM Requirements (U.S.)
Every marketing email must include:
1. **Accurate header info** — truthful From/Reply-to
2. **Non-deceptive subject line**
3. **Identification as advertising**
4. **Physical mailing address** → `*|LIST:ADDRESSLINE|*`
5. **Unsubscribe mechanism** → `*|UNSUB|*` (honor within 10 business days)
6. **No purchased lists**

### GDPR Requirements (EU/UK/EEA)
- Explicit opt-in consent (pre-checked boxes don't count)
- Record of consent with timestamps
- Right to access, erasure, and data portability
- Privacy policy linked on signup forms

### Required Footer Elements

| Element | Merge Tag | Required By |
|---------|-----------|-------------|
| Unsubscribe link | `*|UNSUB|*` | CAN-SPAM, GDPR, Mailchimp ToS |
| Physical address | `*|LIST:ADDRESSLINE|*` | CAN-SPAM, Mailchimp ToS |
| Update preferences | `*|UPDATE_PROFILE|*` | Best practice |

If you omit `*|UNSUB|*` or `*|LIST:ADDRESSLINE|*`, Mailchimp auto-appends an unstyled footer. Always include them in your template.

### Unsubscribe Rules
- Must be clear and conspicuous
- Single-click (no login, no extra steps)
- Must work for 30+ days after send
- Cannot require info beyond email address
- Mailchimp adds `List-Unsubscribe` header automatically (enables one-click unsubscribe in Gmail/Apple Mail)

### Physical Address
Must be a valid postal address. Can be street address, P.O. Box, or registered commercial mail receiving address. Configured at Audience > Settings.
