# alittis.github.io — Backlog

Single source of truth for feedback, bugs and tasks. Item ids use the `GHP-` prefix and are
never reused. The implementing commit's subject starts with the item id (`GHP-N:`), which is
what links this file to git history.

**Type**: 🐞 Bug · ✨ Enhancement · ❓ Needs discussion · 🔧 Chore
**Priority**: P1 (soon) · P2 (planned) · P3 (nice-to-have)
**Status**: Triage → Todo → Doing → Blocked → Done

`Triage` when the shape of the work isn't decided, `Todo` when it is. `Blocked` carries its open
question in the item body. Done items stay below for traceability.

---

## Open

### GHP-2 🔧 The repo has a backlog but none of the other `project/` docs — P3 — Todo

- **Problem:** `project/` holds only this file. There is no `ARCHITECTURE.md`, `DEPLOYMENT.md`,
  `OPERATIONS.md` or `STATE.json`, and no `/misc/`, so the mandated repo shape is incomplete.
- **Want:** Either the rest of the scaffold, or a recorded decision that a four-page static site
  does not need it.
- **Grounding:** The whole repo is four hand-written HTML files served by GitHub Pages from
  `main`; there is no build step, no dependency manifest and no deploy script to document.
- **Discussion:** Deferred deliberately on 2026-09-22 — the backlog was backfilled alone because
  the other templates would each have been one line about a site with no build or runtime.
- **Verify:** `ls project/` lists the agreed set, or this item is closed as "not needed" with the
  reason written down.

---

## Done

### GHP-1 ✨ The Kolpa ZAVEDNO support page offers only the Android build — P1 — Done

- **Problem:** `kolpa-alert/index.html` linked Google Play only, although the iOS app has been
  live on the App Store since 2026-07-07. An iPhone visitor arriving from the App Store listing's
  own support URL found no way back to the app.
- **Want:** The App Store listing linked next to Google Play, in the page's existing markup.
- **Grounding:** [`kolpa-alert/index.html:75`](../kolpa-alert/index.html#L75) — the
  "Povezave / Links" list. Store facts from `~/Developer/kolpa_alert_app/project/STATE.json`:
  `ios_app_store_published: true` (confirmed 2026-07-07), Apple ID `6773248657`, live version
  `1.0.6+7`, iPhone-only, iOS 13.0+.
- **Discussion:** No surrounding copy had to change. Both language sections describe a "mobilna
  aplikacija" / "mobile app" without naming a platform, and both FAQs already gave iOS voice
  instructions — the page was never Android-only in prose, only in its links. Device
  requirements were left off the link, matching the Google Play entry, which states none either.
- **Verify:** `curl -sIL https://apps.apple.com/si/app/kolpa-zavedno/id6773248657` returns 200 and
  the page title is "Kolpa ZAVEDNO"; the rendered support page shows both store links.
- **Shipped:** 2026-09-22, commit `GHP-1: link the iOS build from the Kolpa ZAVEDNO support
  page` (`git log --grep '^GHP-1'`) — App Store URL returned HTTP 200 with title
  "Kolpa ZAVEDNO"; page re-parsed, both store links present and correct.

---

## Progress log

<!-- Newest entry at the top. The headline carries the finding, not the activity. -->

- **2026-09-22** — **The support page was platform-neutral in prose and Android-only in its
  links.** A repo-wide grep for `android|ios|app store|kmalu|prihaja` found no "Android only"
  claim anywhere in the four pages; the sole gap was the missing App Store entry in the
  "Povezave / Links" list. Backlog created at the same time with the `GHP-` prefix; this repo had
  no `project/` docs and no item ids in eight commits of history.
