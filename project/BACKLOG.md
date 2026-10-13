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

### GHP-4 🐞 The Terenska beležnica policy describes historical records the app no longer shows — P2 — Done

- **Problem:** §2.7 *Zgodovinski zapisi* said the app bundles 703 Notranjski park records and loads
  their photos from `nadzor.notranjski-park.si` when one is opened. §3 listed that site's operator as
  a recipient. The overlay had been hidden since 2026-05-22, when the records moved into `TB_MOTNJE`,
  so no build since then could open one. narcis-nadzorniki TB-23 (2026-10-13) removed the code and
  the asset.
- **Done 2026-10-13 (owner's call), on both versions:** §2.7 and the §3 line removed, §2.8–§2.10
  renumbered down by one, and every `&sect;` reference remapped. On `main`, *Zadnja sprememba* is
  13 October 2026. On `ghp-3-post-cutover-policy`, the pre-publish comment now names §2.9.
- **Checked:** the headings run without gaps and every `&sect;` reference names an existing heading.
  Neither version mentions *zgodovinsk*, *Notranjsk* or *WordPress* any more.

### GHP-3 🐞 The Terenska beležnica privacy policy is out of date, and the Postgres move changes it again — P1 — Doing

- **Problem:** `terenska-beleznica/privacy/index.html` was last changed on 20 May 2026. Since then
  the app has moved to token login (v1.2.0), gained record deletion, the Območja and Parcele
  layers, place search and a web review. The page also claimed things that were never true: that
  the app does not access the gallery, and that local photos are deleted on sync. It said nothing
  about the EXIF data uploaded with photos. The narcis-nadzorniki NV-259 / TB-46 cutover then
  moves the data from Oracle to the Alittis VPS (Frankfurt), which the policy has to name.
- **Done 2026-10-12, in two versions** (every claim checked against the narcis-nadzorniki code;
  details in TB-46, TB-49 and TB-50 there):
  - **`main`** — today's production: token login, gallery picker, EXIF, Nominatim, GURS and NarcIS
    WMS, the local stores, deletion, the web review and its change log, teammates' visibility. Takes
    effect when pushed.
  - **Branch `ghp-3-post-cutover-policy`** — the same text, plus the Postgres server, the
    journal and backups in NarcIS, Alittis and Hostinger as recipients, and the new login path.
    Pages serves only `main`, so the branch is not live.
- **Open until T0:** fill in the four `[DATUM PREHODA]` placeholders on the branch, re-check §2.1,
  §2.9 (§2.10 before GHP-4) and §3 against what was built, merge to `main` and push together with the phone release.
  Any change to `main` before then is repeated on the branch.

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
