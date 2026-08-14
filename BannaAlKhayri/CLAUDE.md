# BannaAlKhayri WordPress Project

This file is auto-loaded by Claude Code at the start of every session whose working
directory is this folder (or a subfolder of it). Always launch Claude Code from
`D:\P\A2ZSystems\BannaAlKhayri\ClaudeArtifacts` (or `cd` into it) so this context
loads automatically — no need to re-explain the project in a new session.

## Project

WordPress site for BannaAlKhayri, hosted on Hostinger. Hostinger account is
`contact@bannaalkhayri.org.uk` (accessed in this session via a Hostinger
support/reseller "Impersonate mode" session — confirm this is expected access on
your end if a future session sees the same banner).

Account also owns (not otherwise in scope unless asked): `bannaalkhayri.org`,
`gazabeyondtherubble.com`, `voicesfromgaza.org`.

## Sites

**IMPORTANT — which site is which:**
- `https://pink-curlew-962546.hostingersite.com/` is the **main/real site** — the
  one that matters, content edits and real debugging happen here.
- `https://silver-pony-466242.hostingersite.com/` holds the theme's original,
  untouched Donat demo import.
- **Role change (2026-08-11, standing until the user explicitly says otherwise):**
  the usual staging/production relationship is flipped for now. `silver-pony` is a
  **reference sample** — the untouched original demo to compare against and copy
  design/structure from, not a disposable test target; do not overwrite its content
  casually. `pink-curlew` is being treated as the working/staging site — it's a
  brand-new setup with no live domain connected yet, so it's fine to edit and
  iterate on directly. Revert to the old default (pink-curlew = production,
  silver-pony = disposable test copy) only if the user explicitly says so.
- Default assumption if the user doesn't specify a site: **pink-curlew**, per the
  above.

### Production
- URL: https://pink-curlew-962546.hostingersite.com (no custom domain connected yet)
- Created: 2026-08-02
- WordPress 7.0.2, PHP 8.3
- Path on server: `$HOME/domains/pink-curlew-962546.hostingersite.com/public_html`
- Plugins: WooCommerce, Elementor, Contact Form 7, All in One SEO, Give (donations),
  WPForms, LiteSpeed Cache, Hostinger AI Assistant, and others (`wp plugin list` for
  current state — don't trust this list once it drifts)
- Daily backups enabled (Hostinger-managed)
- `WP_DEBUG` = true, `WP_DEBUG_LOG` = true, `WP_DEBUG_DISPLAY` = false (enabled
  2026-08-03). Log at `wp-content/debug.log`. A timestamped backup of the original
  `wp-config.php` sits next to it on the server from before this change.

### Staging (clone of production)
- URL: https://silver-pony-466242.hostingersite.com
- Created 2026-08-03 via Hostinger's "Copy Website" feature (full file + DB copy from
  production). Site URL/home options were correctly rewritten to the staging domain
  by Hostinger's tool — confirmed via `wp option get siteurl/home`.
- Path on server: `$HOME/domains/silver-pony-466242.hostingersite.com/public_html`
- SSH access confirmed working here too (2026-08-03) — same server/account as
  production, so the `bannaalkhayri` SSH alias and the `claude-code-bannaalkhayri`
  key already reach it. Hostinger's per-site "SSH keys" list in hPanel shows the same
  key under both sites' Advanced > SSH Access pages, confirming it's account-wide, not
  per-site. Just point `wp --path=` at the staging path above — no separate
  credentials needed.
- Re-sync anytime via hPanel > production site > Website > Copy Website (overwrites
  staging with fresh production data — it will warn about staging data loss, which is
  expected/fine).

## SSH access

- Alias configured on this machine: `ssh bannaalkhayri` (entry lives in
  `~/.ssh/config` on this Windows machine, i.e. `C:\Users\waqas\.ssh\config` —
  username on this machine is `waqas`, not `WaqasHaneef` as an earlier session's
  notes assumed)
- Host: 82.29.188.177, Port: 65002, User: u660690591
- Key: dedicated ed25519 keypair at `~/.ssh/bannaalkhayri_hostinger` (private key
  never leaves this machine; public key registered in Hostinger hPanel under
  Advanced > SSH Access > SSH keys — hPanel auto-suffixed the name to
  "claude-code-bannaalkhayri-2" since a key named "claude-code-bannaalkhayri" was
  already registered from a prior machine/session; that older key is not usable
  from this machine)
- Regenerated 2026-08-06 from a fresh machine (`waqas` user) that had no prior
  `.ssh` directory — connection confirmed working.
- WP-CLI is available on the server — always pass `--path=` since there are now two
  WordPress installs under the same account.

## Working conventions for this project

- **Never edit production directly for anything non-trivial.** Reproduce/test on
  staging (silver-pony-466242) first, then apply the same change to production.
- Before editing any file on the server (wp-config.php, theme/plugin files), make a
  timestamped backup copy alongside it first (see the wp-config.php precedent above).
- Content edits: prefer `wp post|page|media` WP-CLI commands over direct DB edits.
- Debugging: tail `wp-content/debug.log` on the relevant site; `WP_DEBUG_DISPLAY` is
  intentionally off so production visitors never see raw errors.
- No custom domain is connected to production yet — if/when one is, urls above will
  change; update this file when that happens.

## Artifacts folder layout

- `notes/` — freeform working notes from sessions (add dated files as needed)
- `logs/` — pulled copies of debug.log or other diagnostic output worth keeping
- `backups/` — local copies of anything pulled off the server before risky edits

## Session log

- 2026-08-03: SSH enabled + key-based auth set up; WP_DEBUG/WP_DEBUG_LOG turned on
  (display off); staging clone created via Copy Website. This CLAUDE.md created.
- 2026-08-03: Confirmed SSH access to staging works with no extra setup (account-wide
  SSH, same key/alias as production).
- 2026-08-06: New session on a different Windows machine (user `waqas`) with no
  existing SSH setup. Generated a fresh ed25519 keypair, registered the public key
  in hPanel (saved as "claude-code-bannaalkhayri-2" due to a name collision), added
  the `bannaalkhayri` alias to this machine's `~/.ssh/config`, confirmed connection.
- 2026-08-06: Built Phase 1 (9 pages per `Requirments.txt` / `WebsiteContent.md`)
  directly on **pink-curlew (production)**, at the user's explicit direction —
  since pink-curlew isn't linked to a live domain yet, the usual staging-first rule
  was waived for this task. silver-pony (staging) was left untouched.
  - Site was found running the purchased "Donat" Elementor charity theme with a
    large ThemeForest demo import already in place (Home One–Seven, Shop, Team,
    Blog, etc.) — not a blank install.
  - No browser/GUI tool is available in this environment, so pages were built as
    native Gutenberg block content (not Elementor JSON), styled via one custom CSS
    pass keyed off the Donat theme's real brand variables from
    `wp-content/themes/donat/assets/css/style.css` (`--theme-color: #1A685B` etc,
    Nunito/Nunito Sans) — pushed through WordPress's Additional CSS
    (`wp_update_custom_css_post()`).
  - Repurposed pages 84 ("Home One" → Home), 203 ("About" → About Us), 3832
    ("Donate Now" → Donate, slug `donate`), 51 (Contact) — cleared their Elementor
    postmeta first. New pages created for Our Story, How We Work, Islamic Giving,
    Orphan Sponsorship, plus an "Appeals" stub parent + Where Most Needed child.
  - Primary Menu rebuilt from ~25 demo items down to the Phase 1 structure.
  - Donate page: created a clean Give form (ID 7929, "Donate to Banna Al Khayri",
    levels £10/£25/£50/£100/£250 + custom amount) — note Give's
    `_give_logged_in_only` meta is inverted (`enabled` = guests CAN donate,
    `disabled` = login required). Fixed `give_settings.base_country` from US to GB.
    Give is still in **test mode with no payment gateway connected**; Give
    Recurring (for true monthly billing) is not installed.
  - Full backup of the 4 repurposed pages' pre-edit content/meta saved to
    `backups/pre-phase1-20260806-*.json` before any changes.
  - See conversation for the full end-of-build checklist (figures needing
    Treasurer sign-off, Zakat/safeguarding content needing professional review,
    payment gateway + monthly giving + Zakat-category form fields still to
    configure).
  - **Follow-up same day**: a visual browser check (via the Claude in Chrome
    extension — multiple browsers were connected to the account, had to pick one
    via `switch_browser`) caught that the site-wide header and footer were still
    100% unedited "Donat" theme demo content (fake NYC address/phone/
    info@donat.com, generic FB/Twitter/YouTube/LinkedIn social icons, a
    WooCommerce cart + search icon, a duplicate donate button pointing at the
    theme author's demo domain, a stock photo of children on every page's title
    banner, and a stuck preloader overlay with ghost "Donat" watermark text) —
    entirely outside what the page-content build touched, since header/footer
    render from two separate Elementor templates (post 72 = header, post 37 =
    footer) selected via Redux theme options
    (`donat_opt('donat_header_select_options')` /
    `donat_opt('donat_footer_builder_select')`), not from page content.
    Fixed by editing each template's `_elementor_data` JSON programmatically
    (json_decode → edit → wp_json_encode, not manual string edits) with real
    contact details/socials, a text-based "Banna Al Khayri" placeholder logo
    (SVG, uploaded to media library, dark + white variants), disabling the
    `cart_enable`/`search_enable` widget settings, fixing the "Quick Links" /
    "Our Service" footer menus (real WP menus `quick-link`/`service-menu`, just
    needed real items), and overriding the stock-photo page-banner background
    via the custom CSS (`.breadcumb-wrapper.background-image`) instead of touching
    theme files. Disabled the preloader via `donat_opt('donat_display_preloader')`.
    **Gotcha**: after editing `_elementor_data` directly via WP-CLI, changes did
    not appear live even after `wp litespeed-purge all` + object-cache flush —
    needed `wp elementor flush_css` too (Elementor's own CSS/render cache is
    separate from LiteSpeed's page cache).
- 2026-08-10/11: Rebuilt the Home page (post 84) as a real multi-section
  Elementor document — the Aug 6 Phase 1 build had cleared page 84's
  `_elementor_data` and replaced it with plain Gutenberg `wp:html` blocks, but
  left `_elementor_edit_mode: builder` / `_wp_page_template:
  template-builder.php` in place. That mismatch meant "Edit with Elementor"
  always flattened the whole page into one Container + one Text Editor widget
  (found and deleted an unpublished `84-autosave-v1` revision, ID 7965, that
  had already been saved in exactly that flattened state — never published,
  so the live site was never actually affected).
  - Fix: wrote a PHP generator (`wp eval-file`, same json_decode/edit/encode
    discipline as the header/footer fix) that rebuilds `_elementor_data` as 11
    real named Containers (Hero, Trust Bar, What We Do, Our Story, Current
    Appeal, Impact Stats, Field Updates, Ways to Give, Newsletter, Quick
    Links) using core Elementor widgets (`heading`, `text-editor`, `button`,
    nested `container` for repeating cards), populated with the exact
    existing Phase 1 copy — not the original Donat demo's stock
    testimonials/countdown/blog filler.
  - Tested first on a disposable duplicate page on silver-pony (staging),
    per the usual convention, before touching production.
  - **Gotchas hit and fixed**: (1) a PHP function named `stat()` fatal-clashed
    with the built-in `stat()` — rename any such helpers; (2) passing an
    already-array `$url` into a function that wraps it in another
    `array('url' => $url, ...)` double-nests the Elementor "link" control and
    crashes `esc_url()` deep in Button rendering — Elementor's frontend
    render swallows this per-widget and silently truncates the rest of the
    page, so a "content just stops halfway down" render is worth checking
    `debug.log` for a fatal, not assuming a data problem; (3) CSS Grid rules
    (`display:grid; grid-template-columns:repeat(auto-fit,minmax(...))`) used
    by the original Phase 1 `.p1-trustbar/.p1-tiles/.p1-stats/.p1-ways`
    classes need their item children to be **direct DOM children** — nested
    Elementor Containers still satisfy this (Elementor containers nest
    directly, unlike widgets which get an extra `.elementor-widget-container`
    wrapper), but relying on Elementor's own per-element width settings to
    land correctly is fragile; switched those 4 rules to `display:flex;
    flex-wrap:wrap` with `!important` flex-basis/min-width on `> div` instead
    — safe for both the old raw-HTML shape and the new Elementor shape.
  - Backup of pre-rebuild post 84 (post_content + all postmeta) saved to
    `backups/pre-elementor-rebuild-20260810-post84.json`.
- 2026-08-11: The granular-widget rebuild above, while structurally sound, still
  didn't look like the purchased Donat theme's actual imported demo — user wants
  the Home page to genuinely match the original "Home One" design, not a
  custom-CSS reinterpretation. Flipped site roles (see Sites section above:
  silver-pony = reference, pink-curlew = staging) and copied silver-pony's
  original, untouched page 84 `_elementor_data` (57,261 bytes, all 24
  theme-specific `donat*` widgets — banner slider, service, about, cta, story,
  team, video, testimonial, project, faq, blog) verbatim onto pink-curlew's post
  84. Confirmed both sites share the same active Elementor Kit (ID 8), so
  global colors/fonts resolved correctly with no extra work. Post-apply
  comparison of widget-type counts between the two live pages is an exact
  match (only header-level `donatmegamenu` differs, expected since the header
  template was already intentionally customized earlier). No new PHP errors.
  Backup of pink-curlew's pre-overwrite state (the granular-widget version)
  saved to `backups/pre-demo-restore-20260811-post84.json`. Home page content
  is now the **unmodified demo content/images/copy** (real branding only in
  the header/footer, which were fixed separately) — swapping in real Banna Al
  Khayri copy, images, and trimming demo-only widgets (fake testimonials,
  countdown, client logos, blog) into each section is follow-up work, not yet
  done.
- 2026-08-11 (same day, follow-up): user clarified the granular-widget rebuild
  wasn't what they wanted either — they want the Home page to look like the
  real demo (confirmed by comparing against silver-pony's "Home One"), just
  with real content swapped into the relevant sections and demo sections left
  in place (not deleted) for manual review. **Standing role flip**: silver-pony
  is now the reference sample, pink-curlew is being treated as staging (see
  Sites section) — this session edited pink-curlew directly without a
  staging-first pass, per explicit instruction.
  - Identified exact widget IDs to target by inspecting silver-pony's real
    `_elementor_data` locally with a small Node inspection script, then wrote
    a PHP `wp eval-file` script (`json_decode` → find-by-id → merge new
    settings → `wp_json_encode` → `update_post_meta`) that only overwrites
    specific settings fields on specific widgets, leaving images/layout/
    animations and unrelated sections untouched.
  - **Real content swapped in**: Banner slider (2 real slides: hero headline +
    "Give once/monthly/Zakat", linking to `/donate/` and `/our-work/`);
    Service section title + the 6 real programme cards (Emergency Relief,
    Food Assistance, Clean Water, Shelter, Orphan Support, Children &
    Wellbeing) replacing the demo's 3 generic service cards; About section
    title/description + the 4-item features checklist replaced with the real
    trust-bar claims (charity number, delivery model, tanker count, reporting
    commitment) + button → `/our-work/`; the CTA section's heading; "cta two"
    banner strip → real appeal messaging + `/donate/` button; Story section
    title/subtitle → the real "eleven households" narrative + Um Kareem quote.
  - **Gotcha**: PHP functions returning array references need `function
    &name(...)` (ampersand before the function name, not just on the
    parameter) — omitting it produces "Only variables should be assigned by
    reference" notices and silently mutates copies instead of the real tree,
    so the update looks successful (no fatal, `wp_json_encode` succeeds) but
    nothing actually changes. Always verify a content swap by grepping the
    freshly-written `_elementor_data` for the new strings before trusting the
    success message.
  - **Correction/flag for manual review**: the `donatgivrform` widget in the
    donation section is NOT a single embedded Give form picker — it renders a
    swiper carousel querying a `donations` custom-post-type for real published
    appeal/campaign posts (title, raised/goal, link). Setting
    `select_give_form` to our real form ID (7929) had no visible effect; this
    section still shows the theme's demo campaign cards because we have no
    real posts in that CPT yet. Needs real costed-appeal posts published
    before this section will show real data — not a simple field swap.
  - **Left as demo on purpose** (no real content exists yet — not dropped,
    per instruction): Team, Video, Testimonial slider, Project grid, FAQ,
    Blog, client logos, countdown timer, and the `donatstory` widget's
    name/years-of-experience fields in the Story section (schema is a
    "founder/staff bio card", doesn't fit a beneficiary quote — flagged for
    the user to decide whether to repurpose or swap for a different widget).
  - Backups: `backups/pre-demo-restore-20260811-post84.json` (pre demo-copy),
    `backups/pre-content-swap-20260811-post84-elementor-data.json` (pre
    content-swap, i.e. pure demo state).
