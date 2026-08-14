# Shique London — SEO Project

Working directory for ongoing SEO work on **shiquelondon.co.uk**, a WordPress site (custom "Stylena" theme) hosted on IONOS. This file is the persistent memory for this project — **update it at the end of every session** (or after completing any task) so work can resume incrementally without re-discovering context.

## Operating Guardrails — read before making any change

This is a live production site, on shared hosting, with no staging environment. These rules apply to every session with SSH/wp-admin access:

1. **Back up before any destructive or bulk change.** Before editing `wp-config.php`, theme files, or running any bulk database operation (comment purge, plugin table cleanup, schema changes), copy the file/table first — the `wp-config.php.bak-20260805` pattern from the environment-type fix is the model; reuse it for every server-side file edit. For anything touching more than a handful of posts/pages/comments at once, note the exact count and IDs affected before running the action, so it's reversible.
2. **Never bulk-delete or bulk-publish irreversible content without flagging it first.** Trashing the 338 spam comments and the Hello World post is low-risk and pre-approved. Treat anything not already pre-approved in this file (deleting orphaned plugin tables, deactivating a plugin, rewriting a live page wholesale) as "flag it, then do it" — add a one-line rationale to the Session Log even if you don't stop to ask first, so the user can review after the fact instead of being surprised.
3. **Verify Google account/property context before every GA4/GTM/GSC/GBP action.** This project already hit one near-miss where the browser session silently switched to the agency's unrelated NextGen Digital account. Confirm the account/property reads "Shique London" / `shiquelondon.co.uk` before saving any change in Analytics, Tag Manager, Search Console, or Business Profile.
4. **Snapshot the metric you're about to move, before you move it.** Before starting each phase (AIOSEO scores, PageSpeed numbers, keyword rankings, GBP metrics), record the current value here or in the session log — otherwise "did this work?" has no baseline to check against.
5. **Test in a logged-out/incognito context before calling anything done** — the same pattern that verified the GA4 fix. WP admin sessions and cache/tracking exclusions can hide problems a real visitor would see.
6. **No content or config change goes live without a one-line note in the Session Log**, even small copy/meta edits — this file is the only continuity mechanism between sessions; undocumented changes are invisible to whoever picks this up next.
7. **AIOSEO is Free/Lite tier — check before promising anything Pro-only** (advanced schema types, redirect manager, additional checklist items). Either scope the task to what Free supports, or flag it as a licensing decision rather than attempting a workaround.

## Access

- **SSH/SFTP access is set up with key-based auth (no password needed)**: Host `access-5018470946.webspace-host.com`, port 22, user `a282748`. An SSH keypair was generated (`~/.ssh/id_ed25519_ionos_shique`) and its public key installed on the server's `~/.ssh/authorized_keys` on 2026-08-05. An SSH config alias `ionos-shique` was added to `~/.ssh/config` — just run `ssh ionos-shique "command"` or `scp file ionos-shique:/path`, no password/prompt required. (A system env var `IONOS_UK_SSH_PASSWORD` was tried first per user preference but isn't visible to tool sessions — likely doesn't propagate to already-running processes on Windows; key auth sidesteps this entirely and is more secure anyway.) Web root: `/homepages/38/d4299262951/htdocs/`, WordPress install: `/homepages/38/d4299262951/htdocs/wordpress/`.
  - `wp-config.php` contains DB credentials and secret keys — never `cat` the whole file (Bash's auto-mode classifier correctly blocks this); use targeted `grep`/`sed -n 'Np'` for specific lines instead.
  - `wp-content/mu-plugins/` is a good spot for temporary diagnostic scripts (loads before regular plugins, not visible in the normal Plugins list) — clean up after use.
  - No PHP error logging is configured on this host (`log_errors` off, no `error_log` path) and `ini_set()` from within WordPress doesn't override it — to capture real PHP errors, write a diagnostic script using `error_log($msg, 3, $customPath)` (the explicit-destination form bypasses php.ini restrictions).
- **WordPress admin access works via Claude in Chrome browser automation.**
  - URL: `https://shiquelondon.co.uk/wp-admin/`
  - Use browser **"Browser 1"** (deviceId `5771aaf5-6f34-4a91-a5c9-64dceedaf046`) — it has an active logged-in WP session for this site (user: Shique London / admin). Select it with `select_browser` before navigating.
  - Do not enter credentials directly; if the session ever logs out, ask the user to log in manually (they can sign in via "Sign in with Google" or WP username/password) and confirm before continuing. There's also a passwordless "Sign in as Shique" Google SSO button on the login page — safe to click, no credential entry involved.
  - There are at least 2 WP admin users on this site (info@shiquelondon.co.uk / "Shique London", and the agency's own waqas.haneef1@gmail.com) — either may end up logged in depending on which Google account the browser session picks; check the admin bar name if it matters.
  - Site Kit's Google OAuth connection is tied to the `info@shiquelondon.co.uk` Google account specifically, which has 2FA enabled (phone approval) — re-authenticating Site Kit modules may require the account owner to approve a prompt on their phone.

## Site Stack

- **CMS:** WordPress 7.0.2, custom theme **Stylena** (built by A2Z Systems — same org as this workspace)
- **SEO plugin:** All in One SEO (AIOSEO) v4.9.10, **Free/Lite tier** (no license key)
- **Analytics/Search:** Site Kit by Google v1.184.0 — Google Analytics + Search Console connected, low/no traffic data so far (site looks newly launched)
- **Other plugins:** Contact Form 7, IndexNow (Bing), Tawk.to Live Chat, WP Migrate Lite, WP-Optimize (installed but inactive), Widgets for Google Reviews (installed but inactive), plus two custom mu-style A2Z Systems plugins: "AI Debug Info" and "DB Cleanup"
- **Content types:** Pages (8), 1 legacy "Hello world!" post, custom post types for Services, Team Members, Portfolio Items, Image Sliders, FAQs

## SEO Baseline (captured 2026-08-04)

See `seo-audit-findings.md` for full detail. Headlines:

- Google Search Console verified & connected directly to AIOSEO; XML sitemap enabled and in sync (`/sitemap.xml` → page/service/post-archive/addl sitemaps). `robots.txt` is clean, no blocking issues found.
- **AIOSEO on-page SEO scores are low across the board**: Home 23/100, Services 23/100, Team 23/100, Membership 23/100, Contact 28/100, About 39/100, Portfolio 42/100 (readability scores are fine, 80-82/100). This is the single biggest quick-win area.
- Titles/meta descriptions are already written for all 7 published pages (reasonable quality, keyword-relevant to "London hair & beauty salon").
- Default **"Hello world!" post is still published** with 338 pending (spam) comments sitting in moderation — should be trashed/cleaned up; spam comment backlog is a minor trust/security housekeeping item, not core SEO, but worth a quick fix.
- Site Kit shows the site has had essentially **no organic traffic yet** — consistent with a newly launched site; no historical ranking data to compare against yet.
- AIOSEO's own "SEO Checklist" is only 6/14 complete — worth reviewing what's outstanding.
- "Action Scheduler: 26 past-due actions" warning appears on every wp-admin page — unresolved background task queue issue, worth investigating (could be a plugin cron problem).
- No Bing/Yandex/Pinterest webmaster verification set up (only Google). IndexNow plugin is installed — check whether it's actually configured/firing.

**Note (2026-08-11): this baseline — 8 pages + Services custom post type, existing titles/metas, low AIOSEO on-page scores — is confirmed as the authoritative picture of the site, superseding an external audit doc that assumed 13 blank service pages. See `strategic-plan-reference.md`'s Reconciliation section for detail.**

## ✅ RESOLVED (2026-08-05): GTM/GA4 snippet wasn't rendering on the live site at all

**Root cause**: `wp-config.php` had `define( 'WP_ENVIRONMENT_TYPE', 'local' );` (line 86) — almost certainly a leftover from initial local development by the build agency (NextGen Digital), never updated at go-live. Site Kit's `Tag_Environment_Type_Guard` class (`wp-content/plugins/google-site-kit/includes/Core/Tags/Guards/Tag_Environment_Type_Guard.php`) only allows tag output (Analytics, Tag Manager, Ads — everything) when `wp_get_environment_type()` returns `'production'`. With it set to `'local'`, Site Kit silently and correctly refused to print any tracking snippet, for every visitor, logged in or out — no error, no warning, exactly as designed. **This is very likely the real reason GA4 has shown ~zero data since this project started, not just low traffic as originally assumed.**

**Fix applied**: commented out that line in `wp-config.php` (backup saved alongside as `wp-config.php.bak-20260805` on the server). `WP_ENVIRONMENT_TYPE` now falls back to WordPress's default of `'production'`.

**Verified working end-to-end** same day: raw `curl` fetch now shows `GTM-NH5JBX47`, `dataLayer`, `gtag(`, and `googletagmanager` all present in the HTML; a real browser (logged out of WP admin) fired an actual `google-analytics.com/g/collect` hit with `tid=G-4WC34Y5X7Y`; GA4 Realtime showed the live session with `page_view`, `first_visit`, `session_start`, `click`, and **`fresha_click` (×3, from earlier test clicks)**.

Full diagnostic trail (in order tried, all ruled out before finding the real cause) — kept for reference in case something regresses:
- Consent mode — off
- WP-level page/object cache — `WP_CACHE` explicitly disabled
- Site Kit's "exclude logged-in users" setting — confirmed via genuinely logged-out sessions throughout
- CDN/edge caching — no `Cache-Control`/`Age`/`X-Cache` headers, fresh origin hits
- Stale Site Kit OAuth connection — fully disconnected/reconnected both Analytics and Tag Manager (incl. 2FA re-auth) — no effect
- Theme code — `header.php`/`functions.php` both clean
- PHP crashes — ruled out via a temporary mu-plugin error/exception/fatal catcher (see Access section for the technique) — zero errors on any page load
- Found via: reading Site Kit's own plugin source over SSH (`GTag.php` → `Tag_Manager/Web_Tag.php` → `Modules/Tag_Manager.php::register_tag()` → its guard chain → `Tag_Environment_Type_Guard`), then grepping wp-config.php for `WP_ENVIRONMENT_TYPE`.

**Also noticed while digging (not yet acted on)**: the site's database has orphaned tables and scheduled cron jobs for a large number of plugins that are **not** in the current active-plugins list — Rank Math, W3 Total Cache, WPForms, ShortPixel, Uncanny Automator, MonsterInsights, UpdraftPlus, WP Mail SMTP, All In One WP Security, Imagify, IONOS Essentials, TrustIndex, User Feedback. Consistent with the site having been built from a template/clone with more plugins, later stripped down to the current 8 — same likely origin as the environment-type bug. Worth a cleanup pass eventually (see Priority Roadmap, Month 1), not urgent.

**Follow-up still needed**: `fresha_click` fired correctly in Realtime but hadn't yet propagated to the standard Events/Key-events admin table as of 2026-08-05 (GA4 processing lag, typically a few hours) — mark it as a Key Event once it appears (Admin → Data display → Events → Key events).

## Analytics & Tracking (captured 2026-08-04)

- **GA4 property**: `509244863` (account `371774500`), Measurement ID `G-4WC34Y5X7Y`. Installed via Site Kit (direct gtag snippet) — Site Kit excludes all logged-in WP users from tracking (confirmed working correctly as of 2026-08-05, now that the environment-type bug above is fixed).
- **GTM container**: `GTM-NH5JBX47` (account `6319595556`) — also installed via Site Kit, live/published as **Version 12** (published 2025-12-04 by `info@shiquelondon.co.uk`).
- **GTM access note**: the correct Google identity for Shique London's GA4/GTM/Search Console is a separate Google account from the agency's own `waqas.haneef1@gmail.com` (which only has access to an unrelated NextGen Digital account) — the browser session occasionally resets to the wrong account; always verify the account/property before making changes (Tag Manager account should read "Shique London" / `shiquelondon.co.uk`, GA4 breadcrumb should read "Shique London"). **See Operating Guardrails #3.**
- **Enhanced Measurement**: was OFF (only `page_view` tracked) — turned ON 2026-08-04, now measuring Page views, Scrolls, Outbound clicks, + 4 more defaults. This auto-captures WhatsApp/Fresha clicks generically as outbound-click events (on top of the named events below).
- **GA4 ↔ Search Console link**: did not exist ("No links yet") — created 2026-08-04, linking `shiquelondon.co.uk` (GSC, Domain property) to the `Website` GA4 stream.
- **CTA click tracking — already built in GTM (pre-existing, ~8-9 months old, live since Dec 2025), not something we needed to add**:
  - `phone_click` — trigger "Phone Button Click" (Click URL contains `tel:`) → tag "GA4 - Phone Click"
  - `whatsapp_click` — trigger "WhatsApp Button Click" (href contains `wa.me` or `whatsapp.com`) → tag "GA4 - WhatsApp Click"
  - `fresha_click` — trigger "Fresha Button Click" (href contains `fresha.com`/`fresha`) → tag "GA4 - Fresha Click" (covers header "Book", per-service "Reserve", and "Reviews" links — all Fresha booking CTAs sitewide)
  - Also pre-existing: `GA4 - Advice Form Submit`, `GA4 - Contact Us Form Submit`, `GA4 - Member Form Submit` (Contact Form 7 submissions)
  - This is the intended proxy for bookings: we have no Fresha API/backend access, so the outbound click to Fresha is the closest signal to "started a booking."
- **GA4 Key Events (conversions)**: `phone_click` and `whatsapp_click` were **already marked** as key events. `submit_form` and `calendly_click` (leftover from a previous booking provider?) are also marked. `user_engagement` was also marked when we first checked (2026-08-04) — fires on nearly every session, which dilutes conversion-rate reporting, so it was **unmarked as a key event same day** at the user's request. **`fresha_click` fired correctly in Realtime on 2026-08-05 but hadn't reached the standard Events admin table yet (processing lag)** — mark it as a Key Event once it appears.
- **Tracking is now confirmed live end-to-end as of 2026-08-05** (see the resolved critical-bug section above) — real traffic data should start accumulating from here on. Revisit reports in a few days to see actual visitor numbers for the first time.

## Priority Roadmap

**Full sequencing lives in `strategic-plan-reference.md`** (Week 1 → Month 6, merged from this file's original backlog plus the Combined 6-Month Plan, corrected against the confirmed live-site structure above). That file is the single source of truth for task order going forward — don't work from a separate flat backlog.

Immediate next actions (Week 1, in order):
1. Clean up the default "Hello world!" post + delete/spam-filter the 338 pending comments (back up comment IDs first — Guardrail #1).
2. Investigate and resolve the "Action Scheduler: 26 past-due actions" warning.
3. Confirm `fresha_click` has landed in GA4's standard Events table and mark it as a Key Event.
4. Fix the "Stylena" vs "Shique London" brand inconsistency in footer/Instagram (scope — full strings only, not the theme name itself — pending final confirmation, see Needs From User).
5. Add a true H1 to the homepage with the primary keyword.
6. Activate the already-installed **Widgets for Google Reviews** plugin — closes most of the "no on-site reviews" content gap immediately, no new plugin needed.

Then proceed into Month 1 (technical foundation) → Month 2–3 (on-page/local) → Month 4 (content) → Month 5 (links/CRO) → Month 6 (reporting) exactly as laid out in `strategic-plan-reference.md`.

## Session Log

- **2026-08-04**: Kicked off project. No SSH/IONOS API access available yet (credentials not retrieved from IONOS panel). Got WP admin access via already-authenticated Chrome session ("Browser 1"). Surveyed plugins, AIOSEO settings (general/webmaster tools/sitemap/search appearance), Site Kit connection status, and all published Pages + Posts with their AIOSEO scores. Wrote this CLAUDE.md and `seo-audit-findings.md` baseline. No changes made to the live site.
- **2026-08-04 (later same day)**: GA4 + Search Console setup, with a focus on tracking phone/WhatsApp/Fresha booking CTA clicks (Fresha backend access is limited, so click-to-Fresha is the booking proxy). Turned on GA4 Enhanced Measurement (was off) and linked GA4 to Search Console (no link existed). Discovered the GTM click tracking for phone/WhatsApp/Fresha (and CF7 forms) was already fully built and live since Dec 2025 — nothing needed building. Found `phone_click`/`whatsapp_click` already marked as GA4 Key Events; unmarked `user_engagement` as a key event at user's request (fires on nearly every session, was diluting conversion metrics). Hit a browser-session hiccup where the tab briefly connected to the wrong Google account (agency's own NextGen Digital GTM) — caught before any changes were made there; resolved by re-verifying the account/property name before every subsequent action.
- **2026-08-05**: Tried to fire a real `fresha_click` test event to unlock marking it as a Key Event — discovered instead that **GTM/GA4 didn't render on the live site at all, for anyone**. Diagnosed extensively via Tag Assistant, raw `curl` fetches, and Site Kit settings; ruled out consent mode, WP caching, admin-exclusion, CDN caching, stale OAuth connection (fully disconnected/reconnected Analytics + Tag Manager, including a 2FA re-auth), and theme code. User provided IONOS SSH/SFTP credentials. Used SSH to read Site Kit's plugin source directly, traced the exact guard logic gating tag output, and found the true root cause: `WP_ENVIRONMENT_TYPE` was hardcoded to `'local'` in `wp-config.php`. Fixed it (commented out, defaults to `'production'`), verified via `curl` and a live browser session that tracking now works end-to-end, including `fresha_click` firing in Realtime. See the resolved critical-bug section above for full detail. Cleaned up all temporary diagnostic files (server-side mu-plugin, local credential file).
- **2026-08-11 (Cowork session)**: User had a separate Cowork/Claude conversation running in parallel, working from two Google Drive docs (`Shique_London_SEO_Audit_v2`, prepared 2026-07-30, and `Shique_London_Combined_SEO_Plan`, updated 2026-08-08) — built a full Word-doc implementation plan from them before knowing this folder existed. On being shown this folder: (1) added `strategic-plan-reference.md` and `Shique_London_SEO_Implementation_Plan.docx` with the Drive docs' keyword/competitor/content-gap data; (2) **resolved the discrepancy between the two audits in the user's favor of this folder's own live-site findings** — the Drive audit's "13 blank service pages" framing is superseded by the confirmed 8-pages-plus-custom-post-type structure with existing-but-low-scoring content; (3) merged this file's original 9-item backlog into one priority-ordered Week 1 → Month 6 roadmap in `strategic-plan-reference.md`, replacing the flat list; (4) added the Operating Guardrails section above (backups, account verification, logging, testing before done, licensing checks) since this session has SSH + wp-admin access to a live production site with no staging environment; (5) moved the open business-input questions (bridal pricing, review-request channel, keyword tool budget, etc.) to `strategic-plan-reference.md`'s bottom section, explicitly deferred — ask each one only when its specific task comes up, not as an upfront batch. User intends to delegate ongoing execution to this Claude Code session/workspace going forward.

## Needs from the user — DEFERRED, do not ask upfront

See `strategic-plan-reference.md` for the full list and rationale. Ask each item only when the task that actually needs it is reached — not as a batch before starting the roadmap above.
