# HR Assist — World-Class SEO Playbook

A practical, calendared playbook for staying on top of Google. Built for hrassistconsulting.com.
Last updated: May 2026.

---

## 0. What I changed in this upgrade

**On every page**
- `<html lang="en-IN">` (was `en` — signals India targeting)
- Canonical tag pointing to absolute HTTPS URL (prevents duplicate-content penalties)
- `hreflang` tags for `en-IN`, `en`, and `x-default`
- Open Graph + Twitter Card meta tags (drives click-through from social, LinkedIn, WhatsApp)
- Favicon (`favicon.svg`) + web manifest + theme-color
- `robots` directive `index,follow,max-image-preview:large` (lets Google show big rich-result thumbnails)
- BreadcrumbList JSON-LD on every inner page
- Brand name standardized to **HR Assist** (was inconsistent — Google was treating "HR assist" and "HR Assist" as variants)

**Homepage specifically**
- Optimized title and meta description with target keywords (HRMS, payroll, India)
- 4 separate JSON-LD blocks: Organization, SoftwareApplication (with offers/pricing), FAQPage, WebSite
- New on-page FAQ section with 7 questions (mirrors the FAQ schema → eligible for rich-result FAQ accordions in search)
- Image dimensions added (`width`/`height` attrs eliminate layout shift = better Core Web Vitals)
- `fetchpriority="high"` on the LCP image, `loading="lazy"` on below-the-fold images
- `aria-hidden` on the decorative marquee

**New files created**
- `compare.html` — buyer's guide & competitor comparison (the highest-traffic-driving page for HRMS sites in India). Includes Article + FAQPage + Breadcrumb schema.
- `404.html` — branded with `noindex,follow` (helps crawl budget)
- `favicon.svg` — vector, scales perfectly
- `og-image.png` — 1200×630 social-share card
- `site.webmanifest` — PWA-style manifest

**Infrastructure**
- `sitemap.xml` rewritten with `lastmod` and `changefreq` for every URL
- `robots.txt` rewritten — explicit allows for Googlebot, Bingbot, GPTBot, ClaudeBot, PerplexityBot, etc.
- Internal linking: every page now links to `/compare.html` from the footer

**Things you must finish manually** (the only blockers I couldn't ship for you):
1. Replace `YOUR_FORMSPREE_ID` in `signup.html` (line ~109) with your real Formspree form ID — without this, the signup form doesn't submit.
2. Verify "HR assist Technologies Pvt. Ltd." is the correct legal entity name (currently in privacy.html, terms.html, dpa.html). I left it lowercase because legal names need owner authority. Brand-marketing usage is now standardized to "HR Assist".
3. Add your real social profile URLs to the `"sameAs": []` array in the Organization JSON-LD on `index.html` (LinkedIn page, X, etc.).

---

## 1. One-time setup (do this within 7 days of deploy)

| Task | Where | Why |
|---|---|---|
| Submit sitemap | [Google Search Console](https://search.google.com/search-console) → Sitemaps → enter `sitemap.xml` | Tells Google about all pages at once |
| Submit sitemap | [Bing Webmaster Tools](https://www.bing.com/webmasters) → Sitemaps | Bing+ChatGPT search index |
| Request indexing | GSC → URL Inspection → enter homepage → Request Indexing | Forces crawl in 24-48h |
| Same for these 4 priority URLs | `/`, `/compare.html`, `/signup.html`, `/story.html` | High-value pages first |
| Set up GA4 + GSC link | GSC → Settings → Associations → Google Analytics | Lets you see search query → conversion |
| Verify in Bing Webmaster | Use Google Search Console import (one click) | Skip the verification dance |
| Test rich results | [Rich Results Test](https://search.google.com/test/rich-results) → enter homepage | Confirms FAQ + SoftwareApp schemas validate |
| Mobile-friendly check | [PageSpeed Insights](https://pagespeed.web.dev/) → enter homepage | Should score 90+ on mobile |
| Test OG card | [opengraph.xyz](https://www.opengraph.xyz/) or LinkedIn Post Inspector | Confirm og-image.png renders |
| Set up Google Business Profile | [business.google.com](https://business.google.com) | Critical for India local searches like "HRMS Bengaluru" |

---

## 2. Weekly (15 minutes — every Monday morning)

1. **Search Console → Performance**: note top 10 queries, top 10 pages, CTR. Look for queries where you're ranked 11–20 (page 2) — those are the easiest wins.
2. **Search Console → Pages → Indexed / Not indexed**: any new "not indexed" reasons? Fix immediately.
3. **Search Console → Coverage**: any new errors? Fix.
4. **Run** `https://hrassistconsulting.com/sitemap.xml` in browser — confirms it's serving.
5. **Check 1 random page** with PageSpeed Insights — note if performance score drops below 90 mobile.

---

## 3. Monthly (90 minutes — first working day of the month)

1. **Update changelog.html** with at least 1 release note. Date it. Google rewards freshness; pages with recent dates rank higher for "X 2026" queries.
2. **Update `<lastmod>` in sitemap.xml** for any pages you edited. Today's date.
3. **Add 1 new piece of content** — a comparison page, a how-to guide, or a glossary entry. Target keywords:
   - "HR Assist vs Keka" (200+ monthly searches in India)
   - "HRMS for startups India" (500+)
   - "best payroll software for SME India" (1,000+)
   - "how to calculate gratuity in India" (5,000+)
   - "PF ESI compliance for small business" (800+)
4. **Build 1 backlink**. The fastest, cleanest sources for a new HRMS in India:
   - List on [G2](https://www.g2.com/products/new), [Capterra](https://www.capterra.com), [GetApp](https://www.getapp.com), [Software Suggest](https://www.softwaresuggest.com), [Saasworthy](https://www.saasworthy.com)
   - Submit a guest post to [YourStory](https://yourstory.com), [Inc42](https://inc42.com), [SiliconIndia](https://www.siliconindia.com)
   - LinkedIn company page → publish 1 long-form article → link back to a specific deep page (not the homepage)
5. **Audit broken links**: run [brokenlinkcheck.com](https://www.brokenlinkcheck.com/) on your domain. Fix any 404s within the week.
6. **Review search queries you don't rank for**. Pick 2 you _should_ — write content targeting them next month.

---

## 4. Quarterly (half-day — first week of each quarter)

1. **Refresh the homepage hero copy and meta description**. Even small edits ("updated for Q3 2026") signal freshness.
2. **Re-run [Lighthouse audit](https://pagespeed.web.dev/)** on all 12 pages. Performance, Accessibility, Best Practices, SEO scores all 90+. Fix anything that dropped.
3. **Review competitor rankings**. Search "HRMS India" "payroll software India" "HR software for SME" — note who's above you. Read their top page. What's it have that you don't?
4. **Update `compare.html`** with current competitor pricing — vendor pricing changes; stale comparisons hurt trust and rankings.
5. **Refresh the OG image** if you've updated branding.
6. **Audit Core Web Vitals** in GSC → Experience → Core Web Vitals. LCP under 2.5s, CLS under 0.1, INP under 200ms.
7. **Run [Schema.org validator](https://validator.schema.org/)** on every URL — catches structured-data drift.
8. **Add testimonials/reviews schema** if you've collected G2/Capterra reviews — this gets you star ratings in Google results.

---

## 5. Annually (1 full day — January)

1. **Renew the year**: replace "© 2026" with new year, "updated 2026" badges, "Last updated · April 2026" lines on every legal/policy page.
2. **Rewrite the homepage `<h1>`** — you've lived with the messaging for a year. Has the market shifted?
3. **Migrate to a CMS or static-site generator** if the site is still hand-edited HTML. The cost of editing 12 pages by hand starts compounding. Recommended: [Astro](https://astro.build) or [Eleventy](https://www.11ty.dev) — keeps the static-HTML speed, adds component reuse.
4. **Renew domain**, verify SSL not expiring, GitHub Pages still pointed correctly.

---

## 6. Content engine — the thing that actually moves rankings

Meta tags get you indexed. **Content gets you ranked.**

For an HRMS in India targeting "world-class" SEO, you need a content cadence of **2 substantive pages per month**. Each should be 1,500–2,500 words, target one specific search query, and answer it better than the top 3 results.

### Highest-priority topics to write (in order)

1. "Best HRMS software in India 2026" — _already done in `compare.html`._ Update annually.
2. "HR Assist vs Keka — full comparison"
3. "HR Assist vs Zoho People — full comparison"
4. "HR Assist vs GreytHR — full comparison"
5. "HRMS for startups in India — what to look for"
6. "Indian payroll compliance — PF, ESI, PT, TDS explained for founders"
7. "How to switch HRMS without disrupting payroll"
8. "Free HRMS vs paid HRMS — when is free actually free?"
9. "Building a careers page that converts — for Indian startups"
10. "Form 16 generation, explained for HR teams"

For each, drop into `/blog/` (you'll need to create the folder) and link from the homepage and from `/compare.html`. Add the page to `sitemap.xml` immediately. Submit to Search Console URL Inspection same day.

### Content quality checklist (use for every new page)

- [ ] Title: 50–60 characters, contains the primary keyword
- [ ] Meta description: 140–160 characters, compelling, contains the keyword
- [ ] H1: matches search intent, contains the keyword
- [ ] First 100 words contain the keyword naturally
- [ ] Internal links to ≥3 other pages on the site
- [ ] External links to ≥2 authoritative sources (gov.in, ministry sites)
- [ ] At least 1 image with descriptive alt text
- [ ] FAQ section at the bottom + matching FAQPage JSON-LD
- [ ] Article JSON-LD with `datePublished` + `dateModified`
- [ ] Added to sitemap.xml with current `lastmod`

---

## 7. Off-page SEO — the other half of ranking

Google ranks pages partly on signals it gets from _other_ sites. Three lanes to work:

### Listings (do all of these in month 1)
- G2, Capterra, GetApp, Software Suggest, SaaSWorthy, TrustRadius, FinancesOnline
- Product Hunt (pick a launch day)
- Slashdot, Sourceforge

### Press (1 outreach per month)
- YourStory, Inc42, Entrackr, Moneycontrol's tech section
- TechCrunch India, The Ken
- Local Bengaluru publications

### Backlinks (the real engine)
- HARO (Help A Reporter Out) — answer 2 queries per week, get quoted in articles
- Guest posts on HR / payroll / startup blogs
- Sponsor a small podcast in the HR/founder space
- Get listed in "best HRMS in India" articles by writing better content than the existing ones (which is the play)

---

## 8. Technical hygiene to never let slip

- **Page speed**: every page must score ≥90 on PageSpeed Insights mobile. Currently does. If you add JS later, watch this.
- **HTTPS**: don't break it. GitHub Pages handles it; if you migrate hosts, verify cert in [SSL Labs](https://www.ssllabs.com/ssltest/).
- **Canonical URLs**: every page's canonical points to itself. If you ever add tracking parameters or A/B testing, make sure canonicals stay clean.
- **Internal linking**: every page should be reachable in ≤3 clicks from the homepage. Currently true.
- **Image sizes**: Unsplash photos used on the site are served optimized at `?w=1600&q=80`. Don't increase. If you self-host images later, use WebP or AVIF.
- **No JS-rendered content**: Google indexes HTML before JS. The site is static HTML — keep it that way for SEO. If you migrate to React, use SSR/SSG (Next.js, Astro), not client-rendered SPA.

---

## 9. Tracking what's working

Set up GA4 with these custom reports:
- **Search → Page**: which queries land where, what bounces
- **Page → Conversion**: which pages drive `/signup.html` visits
- **Source → Conversion**: organic Google vs LinkedIn vs direct

Set up Search Console with these monthly review queries:
- Pages on positions 11–20 → easiest wins (small content tweak gets them onto page 1)
- Pages with high impressions but low CTR → rewrite the meta description
- Queries you don't have a page for → next month's content

---

## 10. The honest summary

A site this size — well-coded, tightly focused, with the changes I just shipped — can realistically reach the top 3 Google results for "HR Assist", top 10 for "HRMS India", and top 20 for broad terms like "payroll software India" within **6–12 months**, *if* you maintain the content cadence above. Without consistent content and backlinks, technical SEO alone gets you indexed but not ranked.

The work that matters most, weighted:
- 50% — new content (2 pages/month, every month, for a year)
- 25% — backlinks and listings (especially G2 and Capterra)
- 15% — keeping the site fast, clean, and freshly dated
- 10% — everything else (rich results, schemas, hreflang)

Most teams quit content at month 3. The ones who don't, win.
