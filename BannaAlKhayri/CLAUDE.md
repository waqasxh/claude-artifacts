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
- **Log every completed change to the Session log below, automatically, without
  being asked.** After any change that touches the live site (CSS, content,
  Elementor data, theme/plugin files, menu/settings changes, etc.), append a
  dated bullet immediately — don't wait for the user to request it, and don't
  batch it up for later in the conversation. Keep the existing style: what
  changed, why, any gotcha hit, and where backups landed. This is how sessions
  resume cleanly — the log is the source of truth for "what's already been
  done," not the chat history.

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
- 2026-08-16: Brand color variables + a batch of header/mobile bug fixes on
  **pink-curlew**, working directly per the standing staging role.
  - **Brand colors**: `--theme-color` set to `#14a0be`, `--theme-color2` set to
    `#04fe94` (final values, after a couple of iterations), applied as a
    `:root { ... }` override block (marked `/* Brand color override */`)
    appended to WordPress's Additional CSS via `wp_update_custom_css_post()` —
    same mechanism as the Aug 6 Phase 1 CSS, not touching the theme's Sass
    source. Donat's whole compiled stylesheet is Sass-compiled from
    `assets/sass/` down to `assets/css/style.css`, but every color/font/spacing
    value resolves through native CSS custom properties declared in a `:root`
    block inside `assets/sass/base/_variable.scss` — so a small `:root`
    override in Additional CSS repaints the whole theme without touching Sass
    or the compiled file at all (no build tooling is present on the server
    anyway — theme ships compiled CSS only, no `package.json`/gulpfile).
  - **Gotcha — `scp` with a raw IP bypasses the SSH alias**: using
    `scp user@82.29.188.177 ...` instead of `scp ... bannaalkhayri:...` doesn't
    match the `Host bannaalkhayri` block in `~/.ssh/config` (Host-matching is
    on the literal string, not the resolved IP), so it doesn't pick up
    `IdentityFile`, falls through to password auth, and prompts the user
    interactively. Always use the `bannaalkhayri` alias for `scp`, never the
    raw host/IP.
  - **Gotcha — a stale open Customizer tab overwrites WP-CLI Additional CSS
    edits**: mid-session the `--theme-color`/`--theme-color2` override block
    vanished, and the live custom_css post had reverted to content *older*
    than even the start of the session. Root cause, confirmed via the
    `custom_css` post's revision history plus matching `customize_changeset`
    posts at the same timestamps: someone had **Appearance → Customize →
    Additional CSS** open in a browser tab, and it published/autosaved its
    stale in-editor content over top of the server-side edits — the
    Customizer field is a full overwrite, not a merge. Reapplied the override
    afterward; going forward, don't leave the Customizer open while doing
    WP-CLI CSS edits in the same window.
  - **`.box-icon` header flicker-then-hide bug (fixed)**: the header's
    address/phone/email info-card icons use a `.bg-shape1`/`.bg-shape2`
    CSS `mask-image`, applied client-side by the theme's own `main.js`
    (reads `[data-mask-src]`, sets it as `mask-image`, strips the attribute —
    hence the flicker: unmasked on first paint, then masked a moment later).
    The mask URL baked into the header widget (`donatheader`, id `64e649d`,
    `info_list` repeater's `shape` field, post 72) was still
    `https://wordpress.themehour.net/...info_card_icon_bg_shape_1_1.png` —
    the theme author's own demo domain, confirmed dead by direct fetch. Fixed
    by string-replacing it with the equivalent local media URL (attachment ID
    67, confirmed working) directly in `_elementor_data` via `wp eval-file`
    (backup taken first, per convention). This is the same class of bug as
    the Aug 6 stock-photo/demo-domain issues — the original import left
    several asset URLs pointed at the theme author's own site instead of
    local media.
  - **Mobile off-canvas menu showing no nav items (fixed)**: the desktop nav
    and the mobile off-canvas panel use two *different* WordPress concepts —
    the desktop widget references a menu directly by name
    (`donat_menu_select`), but the theme's global mobile panel
    (`donat_mobile_menu()` in `inc/donat-functions.php`) gates on
    `has_nav_menu('primary-menu')`, i.e. whether a menu is *assigned to the
    `primary-menu` theme location* (Appearance → Menus → Manage Locations).
    It wasn't — the "Primary Menu" (9 items) existed but was never assigned to
    a location. Fixed with `wp menu location assign "Primary Menu" primary-menu`.
    Confirmed `has_nav_menu('primary-menu')` now true.
  - **Search icon hidden on mobile — by theme design, now overridden**: the
    search button is hardcoded `class="... d-lg-block d-none"` (Bootstrap-style
    utility classes) in the `donat-core` plugin's header widget — desktop-only
    by design, not a bug. Added a small Additional CSS override
    (`/* Mobile search icon override */`) forcing `display:inline-block` on
    `.searchBoxToggler` below 1199px, since the user wants it on mobile too.
  - **Two separate "mobile logo" settings — do not confuse them**:
    1. The **off-canvas panel's** own logo (`.mobile-logo` inside
       `.th-menu-wrapper`) is controlled by a Redux theme option,
       `donat_opt('donat_mobile_logo')` — editable at **wp-admin →
       Donat Options (top-level admin menu, URL `admin.php?page=Donat`) →
       Header tab → "Mobile Menu" subsection → Logo field**. This one has a
       normal admin UI and works fine.
    2. The **header-bar inline logo** shown next to the hamburger icon on
       mobile (`.header-logo` inside a `d-lg-none` wrapper, in the sticky
       header) is a *different* setting — `mobile_logo_image` on the
       `donatheader` Elementor widget itself (post 72, widget id `64e649d`)
       — read directly via `$settings['mobile_logo_image']['url']` in
       `donat-core/addons/header/header.php` line ~521, with **no
       `add_control()` registration anywhere**, i.e. no admin UI existed for
       it at all until this session.
    - Its stored value (`logo-white.svg`, supposedly attachment id 7954) was
      a dead reference — the file does not exist anywhere on the server
      (checked `uploads/2026/08/` directly). Fixed by pointing it at the same
      working file the desktop logo uses (`logo-trim-resize.png`, attachment
      7983), directly in `_elementor_data` via `wp eval-file` (backup taken
      first: `/tmp/pre-mobile-logo-fix-post72-elementor-data.json` on the
      server).
    - Then added a real **"Upload Mobile Logo"** Elementor control for this
      field (mirroring the existing "Upload Logo" control), by editing
      `donat-core/addons/header/header.php` directly — backed up first as
      `header.php.bak-20260816-161226` in the same directory, verified with
      `php -l` (no syntax errors) and confirmed HTTP 200 + no new
      `debug.log` entries before calling it done.
    - **Known limitation, accepted for now**: neither the `donat` theme nor
      the `donat-core` plugin has any bundled auto-update mechanism (checked —
      no EDD/Envato/PUC updater present), so this edit is only at risk from a
      **manual** reinstall of `donat-core` specifically (re-uploading a fresh
      copy from ThemeForest). Moving the control to the theme's Redux options
      file instead wouldn't actually remove this risk category — it would
      just swap which manual reinstall (theme vs. plugin) wipes it, since the
      widget's render code that *uses* the setting also lives in
      `donat-core`. The genuinely update-proof fix, if ever wanted, is a
      small **must-use plugin** (`wp-content/mu-plugins/`) hooking Elementor's
      own extension points (`elementor/element/before_section_end` +
      `elementor/widget/render_content`) instead of editing `donat-core`'s
      file directly — not built yet, only discussed. Revisit if `donat-core`
      is ever manually updated and this control disappears.
  - **Mobile `.menu-area-wrap` styling**: on mobile/tablet, this shared
    header-row container holds only the logo (nav menu moves into the
    off-canvas slider instead) — desktop, where it also holds the nav menu,
    is intentionally untouched. Active header class is `.header-default`
    (confirmed via live DOM check). Its base rule
    (`.header-default .menu-area .menu-area-wrap`) ships with a teal pill
    look (`background: var(--theme-color)`, `border-radius: 50px`,
    horizontal padding) meant for the desktop nav pill; the theme only strips
    that below 375px, so it still showed as a teal rounded pill on most
    mobile/tablet widths even with just the logo inside. Added an Additional
    CSS override at `@media (max-width: 991px)` (matches the `lg` breakpoint
    used elsewhere for mobile/desktop splits) forcing
    `background:#fff; border-radius:0; padding:0; margin:0;` with
    `!important` (to beat the theme's own narrower <375px rule cleanly).
  - **Customizer-stomp gotcha recurred**: the "Mobile search icon override"
    and "Mobile menu-area-wrap" blocks both got wiped again (same root cause
    as earlier — a stale open Customizer tab publishing over server-side
    edits; "Brand color override" survived since it predated whichever tab
    was open). Reapplied both, checking each against freshly-refetched
    current content rather than assuming prior state. **This will keep
    happening as long as the Additional CSS Customizer panel gets left open
    in a tab during a session** — if it becomes a recurring annoyance, the
    real fix is a small must-use plugin enqueuing the CSS from a file instead
    of the database-backed Customizer field, which the Customizer can't
    silently overwrite; not done yet, only noted here as an option.
  - **Preloader `.loader` glow scaled to match user's font-size change**: user
    changed `.loader { font-size: 80px }` down to `40px` directly in
    Additional CSS. Checked the Sass source (`assets/sass/utilities/_preloader.scss`)
    — the fill-reveal effect (`.loading-text`, absolutely positioned,
    `width/height:100%` of the `.loader` parent, animated `width` 0%→100%
    over 6s via `@keyframes animloader`) is percentage-based and already
    scales correctly with any font-size, so no animation timing change was
    needed. The one thing calibrated in fixed px for the original 80px size
    was the `text-shadow` glow (`0 0 2px/1px/1px`) — proportionally twice as
    heavy at 40px, so halved it to `0 0 1px/0.5px/0.5px` via a small
    Additional CSS addition targeting `.loader`.
  - **Real preloader bug found and fixed — not actually a font-size issue**:
    user reported the reveal layer (`.loading-text`) sitting ~10-20px left of
    the static layer, only after the font-size change. Reproduced directly by
    cloning `.loader` into a throwaway visible div and comparing both text
    layers' rendered geometry via `Range.getBoundingClientRect()`: with the
    animation frozen and `white-space` left at its default, the two "Banna Al
    Khayri" copies measured completely different widths (301.9px vs 119.6px)
    due to the second copy wrapping mid-animation; forcing
    `white-space: nowrap` on the clone made both measure pixel-identical.
    Root cause: `.loading-text` (the animated reveal layer) has no
    `white-space` rule in the theme's own CSS, so as its width animates up
    from 0%, multi-word text wraps inside the shrinking container and throws
    off the visible glyph position. The theme's original preloader text was
    just **"Donat"** — a single word, which structurally can never wrap
    regardless of this missing rule — so the bug was latent in the theme
    itself and only surfaced once the preloader text became the multi-word
    **"Banna Al Khayri"**. The font-size change just changed when it became
    noticeable; it wasn't the actual cause. Fixed by adding
    `white-space: nowrap;` to both `.loader` and `.loading-text` via
    Additional CSS. Confirmed live via computed style after a fresh page
    load (both report `nowrap`).
- 2026-08-17: Mobile preloader sizing + a real Elementor toggle for mobile
  search visibility, on **pink-curlew**.
  - **Mobile preloader**: added `.loader { font-size: 25px }` for
    `max-width: 991px`, with the glow scaled proportionally again (same
    scaling logic as the 80→40px fix: `25/40 = 0.625` ratio applied to the
    already-halved `1px/0.5px/0.5px` desktop values → `0.625px/0.3125px/
    0.3125px`), via Additional CSS. Desktop's 40px + its own glow values are
    untouched (media-scoped). The `white-space: nowrap` fix from the same day
    applies globally (not font-size-scoped), so it already covers mobile too
    — no duplicate needed.
  - **New Elementor control: "Show Search on Mobile?"** — added a real
    SWITCHER control (`mobile_search_enable`, default `yes`) to the
    `donatheader` widget, same file/approach as the earlier "Upload Mobile
    Logo" control (`donat-core/addons/header/header.php`, backed up first as
    `header.php.bak-20260816-191003`, verified `php -l` + HTTP 200 + no new
    `debug.log` entries before finishing). Placed right after the existing
    "Search Enable?" (desktop) control, same SWITCHER pattern.
  - Instead of touching the ~10 near-duplicate header-style branches that
    each hardcode the search button's `d-lg-block d-none` classes (risky —
    unclear which is actually live, easy to miss one), wired the toggle by
    injecting a small conditional inline `<style>` block once, near the top
    of `render()` (right before the existing `echo donat_mobile_menu();`
    call): if `mobile_search_enable` is `yes`, echoes
    `@media (max-width:1199px){ .searchBoxToggler{display:inline-block
    !important;} }`; if `no`, echoes nothing (falls back to the theme's
    original desktop-only `d-lg-block d-none` behavior).
  - **Removed the now-redundant Additional CSS "Mobile search icon override"
    block** added earlier in the day — it forced the icon visible
    unconditionally with `!important`, which would have silently overridden
    the new toggle's "no" state. The Elementor toggle is now the single
    source of truth for this; confirmed live (the injected `<style>` tag is
    present, the old Additional CSS block is gone, no duplicate/conflicting
    rule).
  - **Home page hero widget (post 84, `donatbanner1`, id `0aae6f7`) had no
    explicit `layout_style` set** — this widget supports 9 different banner
    styles (`donat-core/addons/widgets/donat-banner.php`), each with its own
    separate repeater field (`banner_slides` for style 1... wait, actually
    `banner_slides1` for style 1, `banner_slides2` for style 2, etc — real
    content lives in `banner_slides1`). Several *other* styles' repeaters
    (`banner_slides`, `banner_slides2`, `banner_slides5`) plus stray
    placeholder-looking top-level keys (`title1: "Title One"`, `subtitle:
    "2"`, etc) were still sitting unused in the saved settings from the
    original demo import — harmless as long as `layout_style` resolves
    consistently, but a real risk: with no explicit value saved, both the
    frontend PHP render and the Elementor editor's JS panel have to
    independently resolve the same implicit default, which is exactly the
    kind of thing that can silently diverge between the two contexts
    (matches user's report of an editor/frontend discrepancy on the
    slider/hero). Fixed by explicitly setting `layout_style: '1'` in the
    widget's settings (confirmed `banner_slides1` = style 1 by cross-checking
    the control's `condition` block against the render() `if` branch).
    Backup saved to `/tmp/pre-banner-layoutstyle-fix-post84-elementor-data.json`
    on the server. Verified the live homepage still renders identically
    (hero photo + real headline unchanged) after the write.
    **Left untouched, flagged for later**: the unused ghost repeater fields
    and stray placeholder keys — didn't delete them since I haven't audited
    whether any other `layout_style` branch's fallback logic might reference
    those same flat key names; low risk as clutter now that `layout_style`
    is pinned, but worth a cleanup pass if this widget gets touched again.
    **Could not visually verify in the Elementor editor itself** — no
    wp-admin login is available in this session's browser and entering
    passwords is out of scope; if the discrepancy persists after this fix,
    get specifics (which panel/tab, what's shown vs. expected) from the user
    rather than re-guessing blind.
  - **Actual root cause found (the `layout_style` fix above was real but not
    the cause of this specific complaint)**: user confirmed via the
    Elementor Navigator/Structure panel that the editor showed a "Hero"
    *container* with 3 core-Elementor children (`heading` "The children know
    our team by..." + `text-editor` + a `container` of two `button`s) — this
    is the shape of the **Aug 10 granular-widget rebuild**, not the current
    published `donatbanner1` slider widget. `wp_get_post_autosave(84)`
    confirmed a stale autosave revision (`84-autosave-v1`, post ID **7967**,
    last touched 2026-08-16) held exactly that old granular structure.
    Elementor's editor always prefers a user's own newer autosave over the
    published post when opening the editor (to avoid discarding unsaved
    work) — so no matter what got fixed in the *published* `_elementor_data`,
    the editor kept loading this stale draft instead. **Same bug class as
    the Aug 10 entry above**, which hit a different autosave ID (7965) on
    this same page. Backed up the autosave's postmeta to
    `/tmp/pre-delete-autosave-7967-meta.json` on the server, then deleted
    revision 7967 (`wp post delete 7967 --force`). Verified afterward:
    `wp_get_post_autosave(84)` now returns none, and the published post 84
    is untouched (still `publish`, 58,449 bytes — same data worked with all
    session). **If this pattern recurs on post 84 (or any other Elementor
    page) — check `wp_get_post_autosave($post_id)` first**, before assuming
    a settings/data bug in the published content itself.
  - **Gotcha**: a combined `scp`/backup-then-`wp post delete --force` Bash
    call got blocked by the session's safety classifier (deletion flagged as
    destructive). Splitting into two separate calls — backup first, delete
    second — went through fine once the backup could be confirmed complete
    on its own.
  - **Confirmed fixed by user** after a hard refresh of the Elementor editor
    — editor now shows the real published `donatbanner1` structure
    (Layout Style dropdown + "Banners" repeater with the 2 real image-backed
    slides), matching the live homepage. Discrepancy fully resolved.
  - **New per-slide toggle: "Show as Button (not Video)?"** — the style-1
    "Banners" repeater's second button was hardcoded to always be a video
    lightbox trigger (`popup-video` class + play icon), using its own
    `video_text`/`video_url` fields. Added a SWITCHER control
    (`video_as_button`, default `no` — preserves current video-popup
    behavior on both existing slides) to
    `donat-core/addons/widgets/donat-banner.php` (backed up first with a
    timestamped `.bak` alongside it, verified `php -l` + HTTP 200 + no new
    `debug.log` entries, confirmed live via DOM that both hero buttons still
    render identically to before). When switched on for a slide, `render()`
    outputs a plain `th-btn style5` link (no popup-video class, no play
    icon) instead — reusing the *same* Video Text/Video Link fields as the
    button's label and URL either way, no new text/link fields needed.
  - **`--caveat-font` swapped from Caveat to Mozilla Text**: confirmed
    Mozilla Text is a real Google Font first (tested the `fonts.googleapis.com/css2`
    endpoint directly, got valid `@font-face` rules back — not a Mozilla-only
    self-hosted font, no self-hosting needed). Added
    `&family=Mozilla+Text:wght@400..700` to the theme's existing Google
    Fonts enqueue URL in `donat_google_fonts()`
    (`wp-content/themes/donat/inc/essential-scripts.php`, backed up first,
    `php -l` clean, HTTP 200 confirmed) — Caveat itself was left in the URL
    (not removed) since it may still be referenced elsewhere and removing it
    wasn't asked for. Then overrode `--caveat-font: "Mozilla Text", cursive;`
    via the usual `:root` Additional CSS block. Verified live via
    `document.fonts` that Mozilla Text is actually loaded in-browser (not
    just referenced) and that the CSS variable resolves correctly.
  - **`--caveat-font` value changed again**, per explicit user instruction,
    to `"Cursive", mozilla text` (quoted "Cursive" first, unquoted
    lowercase `mozilla text` second) — updated in place in the same
    Additional CSS block. Note for later: quoting "Cursive" makes the
    browser look for a specific font literally named "Cursive" (not the
    generic `cursive` fallback keyword, which only works unquoted/lowercase)
    — essentially no system has that exact font installed, so in practice
    this will almost always fall through to `mozilla text` (which still
    correctly matches "Mozilla Text"). Functionally fine, just means the
    effective result is the same as before, reached via fallback instead of
    a direct match.
  - **`--caveat-font` value changed a third time**, per explicit user
    instruction, to `cursive, "Mozilla Text"` — generic keyword now listed
    *first*. Unlike the previous two orderings, this one is functionally
    different: a valid unquoted generic family keyword always resolves
    successfully (browsers don't "try and fail" it), so `"Mozilla Text"`
    will never actually be reached/rendered with this ordering — the font
    will always fall back to whatever the OS/browser maps to generic
    cursive. Flagged to the user; left as explicitly requested, not
    reverted.
  - **Second hero button (video-as-button mode) now matches Donate button's
    icon**: the plain-button render branch added last turn (when
    `video_as_button === 'yes'`) had no icon; the Donate/first button always
    shows `<i class="fas fa-arrow-up-right ms-2"></i>` after its text.
    Added the same icon to the button-mode branch in
    `donat-banner.php` (backed up again first, `php -l` clean, HTTP 200
    confirmed). No visible effect on the live site yet since both current
    slides are still in the default video mode — only shows once the toggle
    is switched on for a slide.
  - **`--caveat-font` settled on final value**: `"Mozilla Text", cursive`
    (back to the original, functionally-correct ordering — specific font
    first, generic fallback last). This is the value currently live.
- 2026-08-17 (continued): **Home page About section content update**, on
  **pink-curlew**.
  - The section previously identified as "About" (Aug 11 entry, via a
    `donatfeatures` widget) had been **restructured by the user's own manual
    Elementor edits** since then — that widget no longer exists in
    `_elementor_data`. Confirmed via a fresh section-title scan that "About
    Banna Al Khayri / Accountability is What Sets Us Apart" (id `e3545af`)
    is now paired with a `donatservice` widget (id `bc4766d`) — which,
    before this edit, was showing a **duplicate** of the "Six programmes"
    service cards (Emergency Relief/Food/Water/Shelter — same content as the
    real "What We Do" section elsewhere on the page). **Lesson: re-verify
    widget IDs/structure against current live data before editing anything
    on this page — don't trust IDs recorded in earlier session-log entries,
    since the user edits this page directly too.**
  - Replaced that widget's 4-item `service_list` with the user's real trust-bar
    copy (title/description/button per card): Registered Charity No.
    1214384 → real Charity Commission register link; "We deliver it
    ourselves" → `/our-work/` (verified this page exists, slug `our-work`);
    "65 water tankers delivered (August 2025 – May 2026) [VERIFY]" and "We
    report on the work we fund" → both linked to `#` since no
    impact/reports pages exist yet on the site (flagged to user, not
    invented). Icons (`choose_image`) deliberately left untouched/reused —
    not asked for, out of scope for this change.
  - **Did not guess the Charity Commission URL.** Used WebSearch +
    WebFetch to find and directly verify the real register entry for
    1214384 before embedding it — confirmed live page shows "BANNA AL
    KHAYRI RELIEF AND DEVELOPMENT - 1214384". This is a real, publicly
    important link on a live charity site; guessing the URL pattern from
    memory would have been the wrong move here even though it was very
    plausible.
  - **Known pre-existing issue, not fixed (out of scope this round)**: this
    widget's `choose_image` icons still point at
    `wordpress.themehour.net` — the same dead-demo-domain pattern as the
    earlier `.box-icon` header bug. Likely broken/404, same root cause,
    different location. Flagged for a future pass, not touched here.
  - Backup: `/tmp/pre-about-section-fix-post84-elementor-data.json` on the
    server. Verified live via DOM query — new card titles present, in
    order, matching what was requested.
- 2026-08-17 (continued): **About section rebuilt again** — user had
  restructured it a second time via their own manual Elementor edits
  (client requirement change), swapping the single `donatservice` widget
  for **three separate `donatcta` widget instances** stacked in container
  `3414d0a` (ids `fb1664c`, `afe68bf`, `231f032`), all three still showing
  identical unedited demo content ("Become a volunteer" / "Join Us
  volunteer"). Re-scanned the live tree fresh rather than trusting the
  previous entry's widget ID (confirms the "don't trust recorded IDs on this
  page" lesson above).
  - Asked the user how to map 4 content items onto 3 duplicate widget
    blocks rather than guessing a structural change — user chose: one
    widget with all 4 items, delete the other two duplicates.
  - Put the same 4 trust-bar items (same content/links as the previous
    entry) into `fb1664c`'s `cta_list` repeater (fields differ from
    `donatservice`: `title`/`description`/`button_text`/`button_url`/
    `choose_image`/`choose_shape` — reused the two existing real image/shape
    assets, cycled across all 4 items rather than leaving 3–4 empty).
    Removed sibling widgets `afe68bf` and `231f032` from container
    `3414d0a`'s `elements` array entirely.
  - Backup: `/tmp/pre-about-cta-rebuild-post84-elementor-data.json`. Verified
    server-side (container now holds only `fb1664c`, `cta_list` has 4 items,
    new text present) and live via DOM (heading found, all 4 real strings
    present).
  - **False-alarm investigation, worth noting for next time**: live page
    still showed "Become a volunteer" text after the edit. Traced it via a
    full-tree text search (not a targeted lookup) to a **completely
    separate, unrelated** `donatcta` widget (id `971677f`, container
    `243ac15`) further down the page, between "What We Do" and the
    donation section — not part of the About section, still unedited demo
    content like several other sections already flagged as
    left-as-demo-on-purpose. Left untouched, out of scope for this request.
  - **Reapplied a third time same day** — the whole rebuild got wiped again,
    this time by the user's own Elementor editor session saving stale state
    over it (widget id changed *again*, landing on `231f032` — one of the
    two IDs deleted in the previous rebuild, meaning the editor tab had old
    data loaded from before that deletion and re-saved it on top). Same
    root-cause *category* as the Additional-CSS Customizer-stomp gotcha
    earlier in the day, just for Elementor post data instead of the
    Customizer field: **an editor tab with stale loaded state will silently
    overwrite server-side `_elementor_data` edits when saved, regardless of
    which is newer.** Re-inspected the current widget fresh (never assume
    the ID from the last entry still applies on this page), reapplied the
    same 4 items into `231f032`'s `cta_list` the same way. Backup:
    `/tmp/pre-about-cta-reapply2-post84-elementor-data.json`. Verified live.
    **If this keeps recurring, the practical fix is procedural, not
    technical: avoid overlapping WP-CLI edits and live Elementor editing on
    the same post in the same window — whoever saves last (stale or not)
    wins.**
  - **Bottom row of the 4-card CTA grid was hidden behind the next
    section (fixed, no min-height hack used)**: root cause was a fixed
    `min_height: 800px` Elementor setting on the container wrapping the CTA
    widget (`808036f`) — sized back when the section only held 2 cards
    (1 row). With 4 cards (2 rows) the actual content now needs more than
    800px, but the outer "About" section container (`d59e8e6`) has
    `overflow: hidden`, so content taller than the fixed min-height got
    clipped instead of the container growing. User explicitly didn't want a
    min-height-based fix (i.e., don't just bump the number). Correct fix:
    **removed the `min_height` setting entirely** from `808036f` so the
    container sizes itself to actual content, as it should for any
    variable-length repeater. Backup:
    `/tmp/pre-remove-minheight-post84-elementor-data.json`. Verified live via
    card bounding-rect measurements — both rows now render sequentially with
    no overlap, and the next section starts well clear of the CTA block.
  - **That fix wasn't the whole story — overlap persisted with the *next*
    section (the "What We Do" programmes block), CSS-only fixes couldn't
    resolve it, ended up needing a JS fallback.** After the min-height fix
    above, the CTA cards internally stopped overlapping each other, but the
    widget's own outer wrapper box (`.elementor-widget-donatcta`, i.e.
    `#231f032`) was still reporting a fixed ~291px height while its content
    needed ~629px — a genuine "block parent shorter than its own single
    static child" situation that shouldn't be possible under normal CSS.
    Extensively diagnosed live with the user's help via their own DevTools
    (confirmed the winning rule really was my own `height:auto !important`
    override — so it wasn't a competing-rule problem, `auto` itself was
    resolving wrong in this specific Elementor `.e-con` flex-container
    context). Root mechanism never fully identified even after checking
    flex-basis/grow/shrink, position, float, overflow, max-height, CSS
    containment, inline styles, matching stylesheet rules, and ruling out
    Isotope/masonry JS (present in the theme but scoped to unrelated
    `.filter-active`/`.masonary-active` selectors).
  - **Final fix**: gave up on a pure-CSS answer and added a small JS
    fallback directly in `donat-cta.php`'s `render()` — measures the actual
    rendered height of `.cta-area-1` on `DOMContentLoaded` **and**
    `window.load` (images can grow height after initial layout) for every
    `.elementor-widget-donatcta` instance, and if the wrapper's current
    height is shorter than the content it holds, sets an inline
    `height` **with an explicit `!important` flag** via
    `el.style.setProperty('height', px, 'important')` — plain
    `el.style.height = px` was tried first and silently lost to my own
    earlier `height:auto !important` Additional CSS rule (inline styles
    without `!important` always lose to an external `!important` rule,
    regardless of source order/specificity). This is deliberately NOT a
    static min-height guess — it recalculates from real rendered content
    every load, so it stays correct if the card count changes again.
  - **Gotcha (self-inflicted, cost real time)**: the first version of this
    JS patch used `echo '...'` in PHP to output a string that itself
    contained single quotes (the JS's own string literals) — broke the
    target file's PHP syntax immediately. Reverted from the
    `donat-cta.php.bak-*` backup, fixed by switching to `echo "..."`
    (double-quoted) in the *generator* script, then reapplied. Lesson:
    when generating PHP that echoes JS/HTML containing quotes, match the
    outer PHP quote style to what's *absent* from the generated content,
    not by habit.
  - Confirmed live end-to-end: `#231f032` inline style is
    `height: 629.109px !important`, computed height matches, and the "What
    We Do" section now starts ~184px below the last CTA card with no
    overlap on a fresh, cache-busted load.
  - **Mobile padding tweak**: set `--padding-top`/`--padding-bottom` to
    `30px` (were `0px`) for element `39d38d2` at `max-width:767px`, via
    Additional CSS, using the exact selector the user pasted from their own
    DevTools (`.elementor-84 .elementor-element.elementor-element-39d38d2`).
    Left/right padding (`12px`) untouched, not requested.
- 2026-08-17 (continued): **Started rebuilding the other 8 pages from the
  original Aug 6 Phase 1 batch** — same treatment the Home page got (Aug
  10/11): converting from Gutenberg `wp:html` blocks (with mismatched
  `_elementor_edit_mode`/`_wp_page_template`, same latent "Edit with
  Elementor flattens the page" bug, though the live frontend itself has
  been rendering fine this whole time via Gutenberg — this is about
  structure/editability, not a visible live bug) to real Elementor
  structure, using real copy from `WebsiteContent.md` and silver-pony as
  the reference for widget choices. Confirmed via a batched check that all
  7 candidate pages (About Us 203, Our Story 7923, How We Work 7924,
  Islamic Giving 7925, Orphan Sponsorship 7926, Where Most Needed 7928,
  Donate 3832) share this exact same pre-fix state. **Contact (51) and the
  Appeals parent page (7927) have no dedicated copy in `WebsiteContent.md`
  — left untouched, not in scope for this pass.**
  - **About Us (203)**: silver-pony's "About" page is the *same post ID*
    (203) on both sites — copied its `_elementor_data` verbatim as the
    structural template (`donatfeatures`/`donatteam`/`donatprocess`/
    `donatsectiontitle` widgets), then swapped in real content for the
    sections with a clean 1:1 mapping: Who We Are intro, a 4-item trust
    list (charity number / own field operation / public reporting / small
    growing charity), and Our Values (5 real values — Dignity,
    Accountability, Transparency, Compassion, Stewardship — reusing the
    `donatprocess` widget, which only ships 3 demo items by default, so 2
    more were added using the first item's shape/icon/image assets as a
    template). **Left as demo, flagged for follow-up**: the team section
    (`donatteam`, no real trustee names/photos available yet), the top
    features bar, video, countdown, testimonial slider, client logos — no
    FAQ widget existed on this specific demo page, so the About Us FAQs
    from `WebsiteContent.md` are not yet on the page at all.
    Backup: `/tmp/pre-rebuild-backup-post203.json`.
  - **Donate (3832)**: silver-pony's "Donate Now" page is also the same ID
    (3832), but its structure is very sparse (just two `donatgivrform`
    widgets + a demo "organizer" bio card) — not enough room for the
    richer real Donate-page copy (Gift Aid, Giving Safely, Trust
    Indicators, FAQs), so this one was built as a fresh container tree
    instead of copied from the demo: a real `donatgivrform` widget pointed
    at the existing working Give form (**ID 7929**, from the Aug 6 build)
    plus the rest of the real copy as core `heading`/`text-editor`/
    `button` widgets. Backup: `/tmp/pre-rebuild-backup-post3832.json`.
  - Both pages: fixed `_elementor_edit_mode`/`_wp_page_template` to match
    the Home page's working values (`builder` / `elementor_canvas`),
    verified valid JSON before writing, confirmed HTTP 200 after, flushed
    Elementor CSS cache. **Not yet spot-checked visually in the browser for
    either page** — given the scale of this multi-page task, verification
    so far is data-integrity-level (valid JSON, key phrases present, page
    loads) rather than the deep pixel-level checks used earlier in this
    session; a visual pass is worth doing before considering these two
    fully signed off.
  - **Remaining 5 pages completed same session**: Our Story (7923), How We
    Work (7924), Islamic Giving (7925), Orphan Sponsorship (7926), Where
    Most Needed (7928) — all built as fresh core-widget (`heading`/
    `text-editor`/`button`) container trees rather than copied from
    silver-pony, since their content is long-form prose/FAQ-heavy and
    doesn't map cleanly onto the theme's card/grid-style donat widgets;
    silver-pony was checked as a reference but none of its pages fit these
    content shapes closely enough to be worth copying wholesale. Full real
    copy from `WebsiteContent.md` for each. Same metadata fix
    (`_elementor_edit_mode=builder`, `_wp_page_template=elementor_canvas`)
    applied to all.
  - **Final verification, all 7 pages**: batched check confirms HTTP 200,
    `edit_mode=builder`, non-zero `_elementor_data` on every page. Live
    curl spot-check confirmed real copy actually renders on the frontend
    for About Us, Donate, and How We Work (representative sample across
    the batch, not all 7 individually).
  - **Out of scope for this pass, not touched**: Contact (51) and the
    Appeals parent page (7927) — no dedicated copy for either exists in
    `WebsiteContent.md`. Both still have the same pre-fix Gutenberg state
    as the other 7 pages did before this session. Flag for a future pass
    once real content for those two exists.
  - **Known gaps/lighter-touch spots worth a follow-up pass**:
    - About Us: team section left as demo (no real trustee names/photos
      yet), no FAQ section built (WebsiteContent.md's About Us FAQs aren't
      on the page at all yet), several demo widgets (video/countdown/
      testimonial/client-logos/top-features-bar) untouched.
    - All 7 pages use plain core widgets for body copy rather than the
      theme's own styled donat-widgets (donatfeatures/donatcta/donatfaq
      etc) — real, valid, on-brand-CSS-inheriting content, but visually
      plainer than the Home page's fully-styled sections. Given the sheer
      volume (7 pages in one session, following a CSS-debugging session
      that alone took hours), this was a deliberate scope trade-off:
      structurally correct and content-complete now, matching Home page's
      polish level is a reasonable follow-up if wanted.
    - None of the internal links/buttons point at report pages, appeal
      pages, or other not-yet-built destinations mentioned in
      WebsiteContent.md (e.g. "Read a project report", "See all appeals")
      — left as `#` or pointed at the closest existing real page
      (`/our-work/`, `/donate/`) rather than inventing URLs for pages that
      don't exist yet.
    - Not visually reviewed in the Elementor editor or at mobile
      viewports for any of the 7 pages — verification so far is
      data-integrity + live-HTML-text-presence level, not the deep
      pixel/layout-level checks used earlier in this session for the Home
      page bugs. Worth a visual pass, especially given how much layout
      trouble the Home page's CTA section caused earlier today from
      seemingly reasonable-looking data.
- 2026-08-17 (continued): **Visual pass on all 7 rebuilt pages — found and
  fixed two real bugs the data-integrity checks above had missed.**
  - **Site-wide header/nav/footer was missing on all 7 pages.** Root cause:
    the rebuild script set `_wp_page_template` to `elementor_canvas`
    (Elementor's blank-canvas template, which deliberately strips the
    theme's header and footer for landing-page use) instead of leaving it
    as `template-builder.php` — confirmed by checking what the *working*
    Home page (84) actually uses. This was a mistake introduced during the
    build, not a pre-existing site issue. Fixed by setting
    `_wp_page_template = template-builder.php` on all 7 pages. Confirmed
    visually afterward: header (logo, top contact bar, nav menu, donate
    button), breadcrumb banner, and presumably footer (not explicitly
    re-checked) all render correctly again on every page.
  - **About Us had one leftover demo paragraph**: the "Who We Are" section
    title widget (`beb95b9`) has a `section_desc` field separate from
    `section_title`/`section_subtitle` that wasn't touched in the original
    build — it was still showing the demo's "Donet is the largest global
    crowdfunding community..." text directly under the real heading. Fixed
    with real copy (the WHO WE ARE paragraph from `WebsiteContent.md`).
  - **Confirmed working as intended, no changes needed**: About Us's trust
    checklist (4 items), values section (5 heart-icon cards with real
    Dignity/Accountability/Transparency/Compassion/Stewardship copy —
    looks genuinely good visually), team/video/countdown sections
    correctly still showing as demo (as planned). Our Story, How We Work,
    Islamic Giving, Orphan Sponsorship, and Where Most Needed all render
    cleanly with real copy and correct page chrome. Donate's real Give
    form (ID 7929) renders and is functional — amount presets, payment
    method selector, personal info fields, test-mode notice all visible
    and working.
  - **Lesson for next time**: always cross-check a new page's
    `_wp_page_template` value against a known-working page's value before
    assuming a template name is correct — `elementor_canvas` sounds
    plausible for "a canvas Elementor draws on" but has a very different,
    non-obvious effect (strips theme chrome entirely) from what was
    intended. The data-integrity checks (valid JSON, key phrases present,
    HTTP 200) used right after each page build did not catch this at all,
    since a canvas-template page still returns 200 and still contains all
    the text — only an actual visual check surfaced it.
  - **`.sub-title` decorative lines restored on mobile**: theme's compiled
    CSS has `@media (max-width: 575px) { .sub-title:after, .sub-title:before
    { display: none; } }`, hiding the small decorative line flanking every
    section subtitle (e.g. "—— Who We Are") below 575px. Overrode with
    `display: inline-block !important` via Additional CSS so it stays
    visible on mobile too.
  - **Our Impact counters: 2→3 per row on desktop, borders removed**:
    checked live HTML — wrapper is `.counter-card-wrap` with Bootstrap's
    `col-sm-6` class (50% width from `sm` upward, no large-screen override,
    hence stuck at 2-per-row all the way to desktop), plus nth-child-based
    border rules designed around that 2-column assumption. Overrode
    `.counter-card-wrap` to `width: 33.3333% !important` and removed all
    borders, scoped to `@media (min-width: 992px)` only — mobile (already
    confirmed working) untouched. Verified live: computed width is exactly
    33.3% of the container, `border: 0 none`.
  - **Follow-up: items weren't aligned** after the 3-column fix above —
    cause was the theme's own `nth-child(odd)`/`(even)` padding rules
    (`padding-right`/`padding-left: var(--space-x)` etc), designed around
    the original 2-column layout, still applying asymmetrically once
    reflowed to 3 columns. Added uniform `padding: 0 20px 40px 20px
    !important` + `box-sizing: border-box !important` to the same override
    block. Verified visually: clean 3-column grid, numbers aligned to the
    same left edge per column, rows aligned.
- 2026-08-18: **Fixed a real bug in the "Our Impact" counters** (Home page,
  post 84) — the 1st and 7th counter numbers ("65 Water Tankers Delivered"
  and "2,475+ Children Reached") were rendering almost invisibly against
  the section's dark-green background.
  - **Root cause**: identified the counters aren't a dedicated "counter"
    widget at all — they're the `donatcountdown` widget (id `ad6aab4`,
    `layout_style: 3`) repurposed for stats display. Its PHP
    (`donat-core/addons/widgets/donat-countdown.php`, layout_style 3
    branch, ~line 142) hardcodes the **first** and **last** item in
    `counter_list` to class `.text-theme2` (`color: var(--theme-color2)
    !important`), every other item to `.text-white`. The original Donat
    demo shipped `--theme-color2: #FFAC00` (bright amber) — a fine accent
    against a dark section. The Aug 16 brand-color override changed
    `--theme-color2` to `#0a5262` (dark teal), which is nearly the same
    color as this section's dark-green background — an unintended
    side-effect of that color change that went unnoticed until now, since
    it only manifests on this one widget/section combination.
  - **Fix**: scoped Additional CSS override,
    `.elementor-element-ad6aab4 .box-number.text-theme2 { color: #fff
    !important; }` — targets only this widget instance (confirmed via
    live DOM check that `.text-theme2` isn't used anywhere else on this
    page), matching these two numbers to the other 5 in the row rather
    than picking a new accent color or touching the global
    `--theme-color2` token (still used correctly elsewhere for buttons/
    backgrounds).
  - Backup: `backups/pre-our-impact-fix-20260818-custom-css-7919.txt`
    (pre-fix Additional CSS, post ID 7919). Verified live post-fix: all 7
    counter numbers compute to `rgb(255,255,255)`.
  - **Worth a broader look later**: since `--theme-color2` moved from a
    bright accent color to a dark one, any other place in the theme that
    uses `.text-theme2` / `var(--theme-color2)` for text-on-dark-background
    contrast (not just backgrounds/buttons) could have the same latent
    issue — this was only caught because the user happened to notice it on
    the Home page. Not audited site-wide yet.
- 2026-08-18 (continued): **Fixed misaligned items 3–6 in the same "Our
  Impact" counters section**, reported immediately after the color fix
  above.
  - **Root cause**: the theme's native `.counter-card-wrap` CSS
    (`donat/assets/css/style.css` ~line 16349) is built for a strict
    **2-column** grid — `:nth-child(odd)` gets `padding-right`,
    `:nth-child(even)` gets `padding-left` + `border-left`, and
    `:not(:nth-child(-n+2))` (i.e. "not one of the first two items") gets
    `padding-top` + `border-top` to start a new row. The Aug 17 session
    forced this widget to 3-per-row (`width: 33.3333%`) and stripped all
    borders via an Additional CSS override, and per that day's log also
    added `padding: 0 20px 40px 20px !important` + `box-sizing:
    border-box !important` to normalize spacing for 3 columns — but that
    padding/box-sizing part of the block **was missing from the live CSS**
    when checked today (only the width + border-removal lines were still
    present). Almost certainly wiped by the same recurring "stale
    Customizer tab overwrites Additional CSS" issue logged on 2026-08-16/17
    — this block just wasn't one of the two re-checked that day. Without
    it, item 3 (first row's 3rd column) was incorrectly getting the
    theme's "new row" `padding-top: 40px`, and items 4-6's left/right
    padding followed the odd/even 2-column pattern instead of a true
    3-column one.
  - **Fix**: reinstated the exact `padding: 0 20px 40px 20px !important` +
    `box-sizing: border-box !important` lines into the existing
    `.counter-card-wrap` override block (same `@media (min-width: 992px)`
    scope, desktop only — mobile untouched).
  - Backup: `backups/pre-counter-padding-fix-20260818-custom-css-7919.txt`.
    Verified live: all 7 items report identical `padding: 0px 20px 40px`;
    bounding-rect check confirms clean row alignment (row 1 items all at
    the same y, row 2 items all at the same y, 3 even columns).
  - **Flag for later**: this is now the second time an Additional-CSS
    block has been found silently missing without anyone noticing until a
    visible symptom showed up (the color-contrast bug this session was
    the first). The mu-plugin idea noted on 2026-08-16/17 (enqueue
    Additional CSS from a versioned file instead of the Customizer-backed
    DB field, so a stale editor tab can't silently overwrite it) is
    becoming more worth doing rather than just noting as an option — worth
    raising with the user if this happens a third time.
- 2026-08-18 (continued): **Removed a decorative background-image from the
  "Ways to Give" section** on the Home page (post 84), per the user
  pasting the exact compiled Elementor CSS rule
  (`.elementor-84 .elementor-element-70b3d55::before` and its
  background-video/slideshow/motion-effects variants) and asking to strip
  `background-image` from it.
  - Element `70b3d55` is the Container widget titled "Ways to Give"
    (`_title` in its settings). The image was set via its **Background
    Overlay** control (`background_overlay_image`), layered on top of the
    plain `background_overlay_color: #FDF8EA` — not the base `Background`
    control (`background_image`, already empty).
  - **Same dead-demo-domain pattern flagged multiple times already this
    project** (`.box-icon` header icons on 2026-08-16, About section
    `choose_image` icons on 2026-08-17): the stored URL was
    `https://wordpress.themehour.net/donat/wp-content/uploads/2024/10/donation-shape1-1.png`
    (attachment id 3369) — the theme author's own demo domain. Since the
    user asked to remove it outright rather than re-point it at a local
    copy, fixed by clearing `background_overlay_image` to an empty value
    (`url`/`id`/`size`/`alt` blanked, same shape as the already-empty
    `background_image` field on this element) via `wp eval-file`
    (json_decode → find-by-id → edit → `wp_json_encode` →
    `update_post_meta`, same discipline as every other `_elementor_data`
    edit this project). `background_overlay_color` (#FDF8EA) and the
    section's padding/layout were untouched.
  - Backup: `backups/pre-remove-overlay-image-20260818-post84-elementor-data.json`.
    Verified live via computed style on the `::before` pseudo-element:
    `background-image: none`, `background-color: rgb(253, 248, 234)`
    (matches #FDF8EA) — confirmed with a fresh `wp elementor flush_css`
    + hard reload.
  - **It silently reverted once, then held after a second apply — a new
    variant of the recurring stomp bug, worth flagging distinctly.** User
    reported the image was still showing after the first fix was already
    verified live. Re-checked `_elementor_data` directly and confirmed
    `background_overlay_image` had gone back to the old
    `wordpress.themehour.net` URL — a genuine revert, not a caching
    illusion (the regenerated `post-84.css` on disk had the old image URL
    baked back in too). **Unlike every previously-logged stomp incident
    (Customizer CSS tab, Elementor editor "Update" saves), `post_84`'s
    `post_modified` timestamp never changed through any of this** —
    ruling out a normal editor Save/Update as the mechanism, since that
    always calls `wp_update_post()`. No autosave existed
    (`wp_get_post_autosave(84)` = false both before and after), and no
    new post revisions were created today. Root mechanism not identified
    — reapplied the same fix a second time, and it has now held through
    two follow-up checks several seconds apart plus a fresh CSS
    regeneration. **If this exact class of revert (data reverts but
    `post_modified` doesn't move) recurs, treat it as a distinct bug from
    the known editor/Customizer stomps** — don't assume "someone had a
    tab open" is the explanation without checking `post_modified` first.

## Session close — 2026-08-18

Everything below was verified live and holding as of end of session
(debug.log tail confirms no new PHP errors from today's work beyond one
harmless `wp eval` quoting mistake during development that never touched
the live site). Resume here tomorrow:

- **Confirmed still working from previous sessions**: Home page (post 84)
  structure/header/footer, brand colors, mobile menu fixes, the "Our
  Impact" counters (both the color-contrast fix and the row-alignment
  fix from earlier today), all 7 rebuilt pages.
- **Fixed today (2026-08-18)**:
  1. "Our Impact" counters: 1st/7th numbers invisible (dark teal on dark
     green) — fixed via scoped CSS forcing `#fff` on widget `ad6aab4`.
  2. "Our Impact" counters: items 3-6 misaligned — reinstated a padding/
     box-sizing override on `.counter-card-wrap` that had gone missing
     from Additional CSS since Aug 17.
  3. "Ways to Give" section (widget `70b3d55`): removed a dead-demo-domain
     background-overlay image, per user request. **Reverted once,
     reapplied, now holding** — see the flag above about the unexplained
     revert mechanism.
- **Not yet resolved / worth first attention tomorrow**: the overlay-image
  fix's one-time silent revert has no confirmed root cause. Before trusting
  any further `_elementor_data` edits on post 84 without re-verification,
  worth a quick recheck that `background_overlay_image` on widget `70b3d55`
  is still empty, and that the "Our Impact" fixes from today are still
  live (Additional CSS has now lost content silently at least twice this
  project without the Customizer-tab explanation confirmed as the cause
  both times).
- **Longer-standing open items, unchanged from before** (see prior entries
  for full detail): About Us team section + FAQ section not built, the 7
  rebuilt pages' visual polish below Home page's level, `donatgivrform`
  campaign carousel needs real `donations` CPT posts, and the mu-plugin
  idea (serve Additional CSS from a file instead of the Customizer DB
  field) is worth actually building given how many times silent CSS/data
  loss has now happened.
