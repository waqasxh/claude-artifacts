# Shique London — Strategic SEO Reference (Drive audit + 6-month plan, reconciled)

Added 2026-08-11 by the Cowork/Claude session, from two Google Docs in the
project's Drive folder (`Shique_London_SEO_Audit_v2`, prepared 2026-07-30, and
`Shique_London_Combined_SEO_Plan`, updated 2026-08-08) plus a full Word
implementation plan built from them. The full `.docx` (14 pages, month-by-month
roadmap with owner/effort/status columns and appendices) is included in this
folder as `Shique_London_SEO_Implementation_Plan.docx` — treat this file as
the condensed, machine-readable extract of it, corrected against the live
site as of 2026-08-11 (see below).

---

## Reconciliation — resolved

The Drive audit (2026-07-30) described 13 separate `/services/*` URL pages
as "empty shells" with no body copy or meta description, and made rewriting
all 13 its top priority.

**That framing is superseded. The live-site investigation in `CLAUDE.md` /
`seo-audit-findings.md` (2026-08-04/05, via actual wp-admin + SSH access) is
the authoritative source of truth for site structure and content state.**
Confirmed reality: 8 published Pages (including one `Services` page) plus a
custom `Services` post type, on a custom theme called "Stylena." Titles and
meta descriptions already exist and are decent quality on all 7 live pages.
The actual problem is AIOSEO on-page SEO scores stuck at 23–42/100 despite
that — an in-content issue (focus keyphrase usage, heading structure,
internal links, image alt text), not missing content.

**Practical effect on the plan below:** every task in the Combined 6-Month
Plan and the audit that assumed "write body copy + meta from scratch for 13
blank pages" is retargeted to **"raise AIOSEO on-page scores on the existing
7 live pages + Services custom-post-type entries, using AIOSEO's per-page
analysis panel to identify the specific failed checks (start with Home,
which scores 23/100)."** The keyword table and content-gap list below are
still valid — they describe topics/pages that are missing or thin, not the
literal 13-page structure — just point the work at the real page inventory
described in `CLAUDE.md`.

---

## Operating guardrails — see `CLAUDE.md`

This file is strategy/content reference only. The operating rules for how to
make changes safely on this live production site (backups, account
verification, logging, testing before calling something done) now live in
`CLAUDE.md`'s **Operating Guardrails** section, near the top — read that
before executing anything below.

---

## Priority Roadmap (consolidated — this supersedes the flat backlog list)

Merges the original `CLAUDE.md` backlog with the Combined 6-Month Plan,
corrected per the reconciliation above. Work top to bottom; each phase's
detailed task-by-task breakdown (owner/effort/status columns) is in
`Shique_London_SEO_Implementation_Plan.docx`.

### Week 1 — Critical fixes
- Clean up the default "Hello world!" post + delete/spam-filter the 338 pending comments (back up comment IDs first per guardrail #1)
- Investigate and resolve the "Action Scheduler: 26 past-due actions" warning
- Confirm `fresha_click` has landed in GA4's standard Events table and mark it as a Key Event
- Fix brand-name inconsistency ("Stylena" vs "Shique London" in footer/Instagram — see Needs From User below on scope)
- Add a true H1 to the homepage with the primary keyword
- Activate the already-installed **Widgets for Google Reviews** plugin to surface ratings on-site (no new plugin needed — it's already there, just inactive)

### Month 1 — Technical foundation
- Open AIOSEO's individual-page analysis on Home (23/100) and log the specific failed checks — this becomes the template for fixing the other 6 pages
- Review AIOSEO's own SEO Checklist (currently 6/14) and close out remaining items
- Confirm IndexNow is actually configured with a key and firing
- Add Bing Webmaster Tools verification (quick win — GSC is already verified)
- Activate the already-installed **WP-Optimize** plugin for baseline performance, then layer in WP Rocket once the user installs it (pull that install forward to this phase — it replaces several manual minify/cache/GZIP tasks in the plan)
- Full site crawl (Screaming Frog), PageSpeed/Lighthouse/mobile-friendly test — specifically check the autoplaying homepage hero video for LCP/CLS impact
- Clean up the orphaned plugin tables/cron jobs (Rank Math, W3TC, WPForms, etc. — listed in `CLAUDE.md`'s resolved-bug section) — housekeeping, not urgent, but do it before it causes confusion in a future audit

### Month 2–3 — On-page SEO, structured data, local SEO
- Fix AIOSEO on-page scores across all 7 live pages + Services custom-post-type entries (per-page, using the Home template from Month 1)
- Implement/verify LocalBusiness, Service, FAQPage structured data (JSON-LD); validate with Google's Rich Results Test
- Trim the FAQ block currently duplicated across 17+ pages down to 1–2 hub pages
- Audit NAP citations; list on Yell, Yelp, ThomsonLocal, Treatwell, Fresha, Bing Places, FreeIndex
- Build the Kensington/W14 location landing page (content gap #1)
- Bridal/occasion package landing page (content gap #2 — **deferred pending pricing details from user**, see below)
- Stand up the post-appointment review-request flow (**deferred pending user's choice of channel**, see below)

### Month 4 — Content production
- Launch a real monthly blog/journal, replacing the default WordPress starter post
- Publish the ready-made differentiation posts: "What is Airtouch?", "Tokio Inkarami vs Keratin Treatment," "Balayage vs Highlights"
- Second location content page (Notting Hill or Chelsea)
- Expand the membership page (terms, FAQ, testimonials)

### Month 5 — Link building, PR, conversion optimization
- Backlink audit, competitor gap analysis, outreach target list
- Local press/editorial outreach
- Booking-funnel mapping and CTA strengthening

### Month 6 — Reporting & next cycle
- Full-period SEO report vs. the Week 1 baseline
- Re-run technical validation
- Document SOPs (weekly GBP/reviews, monthly blog, quarterly technical/citation audit)
- Plan next cycle

---

## Keyword opportunity table (highest-priority subset, from audit v2)

Estimated from competitive positioning — no Ahrefs/SEMrush was connected for
the original audit. Reconnect a real keyword tool before treating these
volumes as more than directional.

| Keyword | Difficulty | Opportunity | Ranking | Recommended content |
|---|---|---|---|---|
| hair salon Kensington | Hard | High | Not ranking | Homepage + new Kensington location page |
| hair salon W14 | Easy | High | Not ranking | Location page targeting W14/Olympia |
| balayage Kensington | Moderate | High | Not ranking | Balayage-related page/section on-page fix |
| Airtouch hair Kensington | Easy | High | Not ranking | Airtouch service entry on-page fix |
| Tokio Inkarami London | Easy | High | Not ranking | Tokio Inkarami service entry on-page fix |
| Japanese manicure London | Easy | High | Not ranking | Japanese manicure service entry on-page fix |
| bridal hair and makeup Kensington | Moderate | High | No page exists | New bridal/occasion package page |
| what is Airtouch hair colouring | Easy | Medium | No content | Blog: Airtouch vs balayage |
| Tokio Inkarami vs keratin treatment | Easy | Medium | No content | Blog/comparison post |
| balayage vs highlights | Easy | Medium | No content | Blog post (top-of-funnel) |
| keratin treatment London | Moderate | Medium | Not ranking | Keratin/smoothing service entry on-page fix |
| best hair salon Kensington | Hard | Medium | Not ranking | Needs review volume first, then homepage opt. |

(Full ~20-row table with difficulty/CPC detail is in the docx Appendix A and
in the `Keyword Research (Internal)` / `Keyword Research (Shared)` Drive docs.)

---

## Content gaps identified in the audit (priority order)

1. **Location-specific landing pages** — Kensington/W14 first, then Notting Hill/Chelsea. High priority, moderate effort.
2. **Bridal/occasion hair & makeup package page** — no equivalent exists; every close competitor has one. High priority, quick win (half day) — blocked on pricing input, see Needs From User.
3. **Treatment explainer / blog content** — "What is Airtouch?", "Tokio Inkarami vs keratin treatment", "Balayage vs highlights." High priority, quick win per post.
4. **On-site reviews and ratings** — currently only an off-site Fresha link; **Widgets for Google Reviews plugin is already installed but inactive** — activating it may close most of this gap immediately. High priority, quick win.
5. **Blog/journal section** — site's only post is the default WP starter (still live with 338 spam comments per Week 1). Medium priority, ongoing effort.
6. **Membership page depth** — currently a single promo banner; needs full terms, FAQ, member testimonials. Medium priority, quick win.

---

## Competitor benchmark (closest 3 matches: same postcode tier)

| Dimension | Shique London | Sébastien Hair | Marnis Salon | GA Salons |
|---|---|---|---|---|
| Service page content depth | Existing copy, low AIOSEO score — needs on-page fixes, not a rewrite | Full descriptions + pricing | Full descriptions + pricing | Long-form, brand-driven |
| Reviews shown on-site | None (off-site link only; fix available via inactive plugin) | 4.9★, 1,958 reviews on homepage | Full testimonial wall | 4.9★, 1,404 reviews + press logos |
| Location pages | 1 (generic) | 1 (detailed) | 1 (detailed) | 6 (multi-neighbourhood + intl.) |
| Blog / content marketing | None (default post only) | None | "Journal" section | "Blog" + national press coverage |
| Bridal/occasion package page | None | Yes (Occasion Styling) | None | Yes (Bridal) |
| Brand consistency | Inconsistent (Stylena vs Shique in footer/Instagram) — theme itself is named "Stylena" per CLAUDE.md | Consistent | Consistent | Consistent |

Other competitors considered (Michaeljohn, Daniel Galvin, Hiro Miyoshi,
Kensington Glam, LY Beauty, Oblique) sit above Shique on scale/heritage or
at a similar boutique tier with comparable gaps. `hk-london.com` was
excluded — it's a real estate consultancy, not a salon.

---

## Tools referenced in the plan not yet confirmed set up on the live site

- **Ahrefs or SEMrush** — for real keyword volume/difficulty/backlink data (audit used estimates only)
- **Screaming Frog or Sitebulb** — full-site crawl for the Month 1 technical audit (desktop tool, run against the public URL — no server access needed)
- **BrightLocal or Whitespark** — citation building/tracking
- **Hotjar or FullStory** — session recordings for the Month 5 conversion-funnel work
- **Bing Webmaster Tools** — only Google is verified; quick win since GSC is already verified
- **WP Rocket** — user confirmed integrating this "sometime"; pulled forward to Month 1 above, since it replaces several manual Month 1 tasks (minify, caching, GZIP/Brotli, lazy loading) — measure the post-Rocket baseline, not pre.

---

## Needs from the user — DEFERRED, ask only when the work reaches that point

These are real blockers for specific downstream tasks, but none of them
block starting the roadmap above. Don't front-load these as a batch of
questions — surface each one in the session log when its task comes up
(e.g. ask about bridal pricing only when Month 2–3's bridal page task is
actually being started), so the user isn't asked to make six decisions
before any visible progress happens.

- **AIOSEO tier**: some advanced items (schema types, redirects manager) may need Pro rather than Free/Lite — confirm before promising them.
- **Keyword tool**: decide whether to purchase/connect Ahrefs/SEMrush or proceed on the audit's estimated volumes.
- **Brand name fix scope**: confirm whether the Stylena/Shique fix is just user-facing strings, or whether the theme itself should be renamed.
- **Bridal/occasion package**: need real pricing/package details before drafting that landing page.
- **Review-request channel**: WhatsApp vs. email vs. SMS vs. in-salon prompt for the post-appointment ask, plus approval of the messaging.
- **Local SEO tool access**: BrightLocal/Whitespark — purchase or handle citations manually.
