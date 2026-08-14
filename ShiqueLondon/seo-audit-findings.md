# Shique London — SEO Audit Findings

Detailed findings log, most recent first. This file accumulates evidence/data; `CLAUDE.md` holds the summarized backlog and session log.

---

## 2026-08-04 — Initial baseline

### Access & environment
- Site: https://shiquelondon.co.uk (WordPress, IONOS hosting)
- WP 7.0.2, theme "Stylena" (custom, by A2Z Systems)
- Checked via WP admin dashboard, no server/SSH access this session

### Plugins installed (10 total)
| Plugin | Version | Status | Notes |
|---|---|---|---|
| All in One SEO | 4.9.10 | Active | Free/Lite tier, no license |
| Site Kit by Google | 1.184.0 | Active | GA + GSC connected |
| IndexNow | 1.0.4 | Active | By Microsoft Bing — verify it's configured |
| Contact Form 7 | 6.1.6 | Active | |
| Tawk.to Live Chat | 0.9.3 | Active | |
| WP Migrate Lite | 1.2.0 | Active | |
| AI Debug Info | 1.0.0 | Active | Custom, A2Z Systems |
| DB Cleanup | 1.0.0 | Active | Custom, A2Z Systems — truncates DB tables on schedule |
| Widgets for Google Reviews | 13.3.1 | **Inactive** | Could help local SEO/trust signals if activated |
| WP-Optimize | 4.6.1 | **Inactive** | Could help page speed if activated |

### AIOSEO — General Settings
- Free/Lite version, no license key entered
- Setup Wizard has not been (fully) completed

### AIOSEO — Webmaster Tools Verification
- **Google Search Console: verified (green check)**
- Bing, Yandex, Baidu, Pinterest, Microsoft Clarity, Google Analytics fields: not verified/empty in this tab (Google Analytics is handled via Site Kit separately)

### AIOSEO — Sitemaps
- Sitemap enabled, "connected directly to Google Search Console and your sitemaps are in sync"
- Sitemap index at `/sitemap.xml` → `addl-sitemap.xml`, `page-sitemap.xml`, `service-sitemap.xml`, `post-archive-sitemap.xml`
- Additional custom URLs manually added to sitemap: `/portfolio/`, `/membership/`, `/services-all/`, `/team-all/`
- Excluded from sitemap: Services #496, Team #500 (specific posts excluded — worth double-checking why)

### AIOSEO — Search Appearance (Global/Home)
- Title separator: `-`
- Homepage title: **"Luxury Hair & Beauty Salon London | Haircuts & Styling"**
- Homepage meta description: **"Premium hair & beauty salon in London offering balayage, keratin treatment, haircuts, extensions, nails, brows, lashes & makeup. Book your appointment today."**
- Knowledge Graph type: Organization ("Shique London")

### robots.txt (clean, no issues)
```
User-agent: *
Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php
Disallow: /?s=
Disallow: /page/*/?s=
Disallow: /search/
Allow: /wp-content/uploads/
Allow: /wp-content/themes/
Allow: /wp-content/plugins/
Allow: /wp-json/
Allow: /wp-includes/
Disallow: /cgi-bin/
Disallow: /trackback/
Disallow: /xmlrpc.php
Disallow: /readme.html
Disallow: /?replytocom

Sitemap: https://shiquelondon.co.uk/sitemap.xml
Sitemap: https://shiquelondon.co.uk/sitemap.rss
```

### Pages inventory + AIOSEO scores (score = SEO score/100, second number = readability/100)

| Page | SEO Score | Readability | Title | Meta Description |
|---|---|---|---|---|
| Home | 23/100 | 82 | Luxury Hair & Beauty Salon London \| Haircuts & Styling | Premium hair & beauty salon in London offering balayage, keratin treatment, haircuts, extensions, nails, brows, lashes & makeup. Book your appointment today. |
| About Us | 39/100 | 80 | About Our London Hair Salon \| Luxury & Professional Beauty | Learn about our hair & beauty salon, expert team, premium services, quality standards and passion for delivering exceptional grooming & haircare experiences. |
| Contact Us | 28/100 | 82 | Contact Our London Hair & Beauty Salon \| Book Appointment | Get in touch with our salon in London for bookings, consultations, directions & availability. Find the nearest salon location & expert stylist recommendations. |
| Membership | 23/100 | 82 | Salon Membership London \| Exclusive Beauty & Hair Packages | Join our membership program for exclusive discounts, priority booking, free services, special rewards & premium beauty benefits. Perfect for regular clients. |
| Portfolio | 42/100 | 81 | Salon Portfolio London \| Balayage, Haircuts, Nails & Makeup | Explore our portfolio of balayage transformations, haircuts, keratin results, nail artistry & bridal/party makeup looks created by our expert London stylists. |
| Services | 23/100 | 81 | Salon Services London \| Hair, Beauty, Keratin, Brows, Nails | Discover our full range of salon services in London — balayage, haircuts, keratin treatment, eyebrow lamination, lash extensions, makeup & professional nails. |
| Team | 23/100 | 81 | Expert Hairdressers & Beauty Artists London \| Our Team | Meet our professional London hairstylists, hairdressers, colour experts, nail artists & makeup specialists dedicated to delivering luxury beauty experiences. |
| Privacy Policy | (draft) | — | Privacy Policy - Shique London | (default WP boilerplate text, unedited) |

**All published pages score in the "poor" range (23-42/100) on AIOSEO's on-page SEO analysis** despite having decent titles/descriptions — the deficiency is likely in-content (focus keyphrase usage, headings, internal linking, image alt text). Need to open the AIOSEO analysis panel on an individual page (e.g. Home) to see the specific failed checks before prescribing fixes.

### Posts
- Only 1 post: default "**Hello world!**" (published 2025/08/01), Uncategorized
- Has 338 pending (spam) comments + 1 approved comment sitting in moderation queue
- No real blog/content marketing presence on the site currently

### Site Kit by Google
- Analytics + Search Console both connected as data sources
- Dashboard shows **no meaningful traffic yet** ("no data to display: your site hasn't received any visitors yet"; referral shown as 100% of the trivial traffic that exists) — consistent with a recently launched site with little organic history
- Key metrics not yet personalized/selected by admin

### Outstanding / unresolved warnings
- **"Action Scheduler: 26 past-due actions found; something may be wrong"** banner appears sitewide in wp-admin — not yet investigated. Could stem from one of the custom plugins (DB Cleanup runs hourly cron) or a third-party plugin's scheduled task queue backing up.
- AIOSEO's own onboarding "SEO Checklist" is at 6/14 tasks completed — haven't yet opened it to see which 8 remain.

### Not yet investigated (queued for future sessions)
- Individual page AIOSEO analysis detail (which checks are failing to cause the low scores)
- Page speed / Core Web Vitals (Site Kit "Speed" tab not opened yet; WP-Optimize is inactive)
- Image alt text coverage across the Media Library
- Internal linking structure between Services/Team/Portfolio pages
- Whether Local SEO / Google Business Profile is linked anywhere
- Custom post type "Services" — correct admin slug wasn't confirmed (`?post_type=services` returned "Invalid post type"); check via the sidebar link directly next time
- IndexNow plugin configuration (is a key actually set?)
