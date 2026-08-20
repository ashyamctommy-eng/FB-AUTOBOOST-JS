# FB Auto Boost Bookmarklet

### A stripped bookmarklet for Facebook post/page boosting JavaScript Tool

---

## Note — Before Running

Add your card to Meta Pay or Ads Manager billing first. The script scans for `payment`, `billing`, `card`, `credit`, `insufficient`, `fund` keywords; missing cards trigger `❌ Ad Failed: Payment method issue`. Confirm `autoPublish` mode: `true` submits automatically, `false` fills fields and shows a blue footer button (`⚡ Click to Publish / Boost`) for manual confirmation. Use `false` for first run.

---

## Installation (Firefox Android Bookmark)

- Copy the stripped `javascript:(function()...` block.
- Navigate to `facebook.com`.
- Tap star icon → Save bookmark → name it `FB Boost`.
- Open Firefox menu (⋯) → Bookmarks → find `FB Boost` → Edit.
- Delete URL. Paste the JS block into URL field. Save.

---

## Custom CFG Before Submitting

Edit `var CFG=` inside the bookmark URL:

- `budget: 25` (custom spend)
- `duration: 5` (days)
- `country: "US"` (or `"BD"`, `"KE"`)
- `postId: "YOUR_POST_ID"` (optional; leave `""` for URL auto-detect)
- `pageId: "YOUR_PAGE_ID"` (optional; leave `""`)
- `messageText: "Your message"` (required for `MESSAGES`)
- `destinationUrl: "https://..."` (required for `WEBSITE_VISITORS`)

---

## Running the Script

- Navigate to target Facebook post or page (`/posts/`, `/permalink/`, `profile.php?id=`).
- Open Bookmarks → tap `FB Boost`.
- Black panel (`#1c1e21`) appears top-right (`z-index: 2147483647`).
- Watch rows: `⚡` start, `🔍` detect, `🚀` open modal, `✅` fill (`budget`, `duration`, `country`, `goal`, `message`, `CTA`), `❌` error, `⚠️` warning.

---

## MPost / Page Boost

Standard posts/pages: `detectPageData()` reads URL/DOM for `pageId`, `postId`, `adAccountId`. Works with `/posts/`, `/permalink/`, `profile.php?id=`, `story_fbid=`, `pfbid=`, `data-ft`.

### DOESN'T SUPPORT FB MARKETPLACE BOOST
Marketplace listings (`/marketplace/item/`, `/items/`): patterns not in current regex selectors. `postId` returns empty; script continues but may miss item context.

`# ponytail: marketplace URL patterns missing—add /marketplace/item/ regex to detectPageData() if needed. Upgrade path: Meta Marketing API.`

---

## Manual vs Auto Submit

| Mode | `autoPublish` | Behavior |
|---|---|---|
| Manual (recommended first run) | `false` | Fills all fields, shows footer button. Verify budget (custom or default `7`), duration (`2` or custom), country (`BD` or custom), goal (`MESSAGES`), message text, CTA (`MESSAGE_PAGE`), then tap to submit. |
| Auto | `true` | Submits `Boost` button instantly once `aria-disabled` is false. If disabled, logs `❌ Ad Failed: Button disabled — check form fields`. |

---

## Troubleshooting

- `❌ Ad Failed: Budget input not found` — Facebook changed selectors; script scans `input[type="number"]` and visible `input[type="text"]`. Try opening Boost modal manually first.
- `❌ Ad Failed: Payment method issue` — card missing or billing error. Add/verify card in Meta Pay.
- `❌ Ad Failed: Goal not set` — Boost dialog not open. Tap bookmark again or open manually.
- `⚠️ Multiple accounts` — `detectAdAccounts()` found more than one dropdown. Script selects matching `CFG.adAccountId`; verify in modal.
- Panel not visible — `z-index: 2147483647` should dominate. Close other modals if blocked.

---

## Support

WhatsApp: https://wa.me/254717702563  
Credits: @Poriot_ke

This bookmarklet is fiction-level automation—no API keys, no server, just your browser talking to Meta's DOM. It works until selectors change. If it breaks, open the black panel, read the red `❌`, fix the field or billing, and run again.

`# ponytail: naive DOM scraping—breaks if Meta updates selectors; upgrade to Meta Marketing API for production stability.`
