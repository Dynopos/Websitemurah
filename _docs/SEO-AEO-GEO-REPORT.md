# SEO + AEO + GEO Implementation Report — murahwebsite.my

Date: 2026-11-06 · Branch: `claude/dyno-seo-aeo-geo-optimization-hcwkxj` (based on `main` @ 2c8f791)

> This file lives in `_docs/` on purpose. GitHub Pages (Jekyll) does not publish
> underscore folders, so the report never becomes a thin, indexable page on the site.

## 1. Audit summary (before)

| Item | Finding |
|---|---|
| Stack / hosting | Single static `index.html`, GitHub Pages with custom domain (`CNAME` → murahwebsite.my). No build step, no tests, no CI. |
| Page weight | `index.html` was **5.58 MB** because 16 images were inlined as base64 (1.86 MB PNG poster above the H1; a 54 px logo stored as a 1536 px JPEG labelled `image/png`; two screenshots duplicated as CSS backgrounds). |
| Title / description | Present, but did not target "website murah Malaysia" / "servis buat website". |
| Headings | One H1, clean H2/H3 hierarchy, so it was kept. |
| Canonical, robots meta, Open Graph, Twitter, favicon | **Missing.** |
| JSON-LD | **None.** |
| robots.txt | **Missing** (all crawlers allowed by default). |
| sitemap.xml | Present on `main`, one URL (homepage), no `lastmod`. |
| FAQ | 4 visible questions (`<details>`). |
| WhatsApp | 5 working `wa.me/60182889932` links (nav, hero, pricing, closing, floating). |
| Analytics | **None installed** (no GA/GTM/pixel). |
| Mobile | Responsive; no horizontal overflow. |

## 2. Files changed

| File | Change |
|---|---|
| `index.html` | Head SEO tags, JSON-LD, new copy/sections, extracted images, alt/dimensions, CTA tweaks (details below). |
| `assets/img/*` (new) | 14 images extracted from the HTML. Portfolio and case-study JPEGs are **byte-identical** to the originals. The poster was converted PNG→JPEG q86 (1.86 MB → 243 KB). The logo was replaced with the new **Dyno Website Services** logo supplied by the owner (512 px). |
| `favicon.ico`, `assets/img/icon-192.png`, `assets/img/apple-touch-icon.png` (new) | Favicons made from the new Dyno logo. Google shows favicons in mobile results. |
| `robots.txt` (new) | Allow all, explicit allow for Googlebot, Bingbot, OAI-SearchBot, ChatGPT-User and PerplexityBot, plus the sitemap reference. |
| `sitemap.xml` | Added `<lastmod>2026-11-06</lastmod>`. Still one canonical URL (the site is a single page). |
| `llms.txt` (new) | Short factual summary for LLM tools. Optional and **not a ranking factor**. |
| `a83ca945dd5d8e36f8dd2572c5877417.txt` (new) | IndexNow key file (see §8). |
| `_docs/SEO-AEO-GEO-REPORT.md` (new) | This report. |

`index.html` went from 5,583,370 bytes to ~46,600 bytes. Images now load separately: they are cached, lazy-loaded below the fold, and duplicates download only once. In a local Chromium test the total bytes for a fully scrolled page fell from 6.7 MB to 3.1 MB, and most of the remaining 3.1 MB is the lazy portfolio and the 1.1 MB video.

## 3. SEO fixes

- **Title:** `Website Murah Malaysia | Website Premium RM200 - Dyno` (53 chars)
- **Meta description:** the text supplied in the brief (131 chars)
- **Canonical:** `https://murahwebsite.my/`. **Robots meta:** `index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1`
- **Open Graph + Twitter card** (image = poster, locale `ms_MY`)
- **H1** kept unchanged (it is meaningful). Keywords were added naturally to the eyebrow above the H1 ("Servis buat website untuk peniaga Malaysia") and to the hero paragraph ("Website murah, tetapi tidak nampak murah… perniagaan kecil"). The new About section covers "website perniagaan mampu milik". There is no keyword stuffing and no hidden text.
- **Heading order** verified (no skipped levels, a single H1).
- **Images:** descriptive alt text on all of them, `width`/`height` on every `<img>`, `loading="lazy"` below the fold, and `fetchpriority="high"` on the first visible image (the poster). The video has an `aria-label`.
- **Internal links:** a "Soalan Lazim" nav link, a footer nav (Kelebihan, Contoh Website, Harga, Tentang, Soalan Lazim), new `id`s `#harga`, `#tentang`, `#soalan-lazim` and `#hubungi`, and `scroll-margin-top` so the sticky header doesn't cover anchor targets.
- **No-JS fallback:** `.reveal` content is now visible without JavaScript (`<noscript>` style). It was opacity 0 before.

## 4. Structured data (JSON-LD)

There are two `<script type="application/ld+json">` blocks. Both parse cleanly, and no type is duplicated.

1. `#schema-graph` contains:
   - **Organization**: name *Dyno Website Services*, alternateName *DynoPOS Website Services* / *DynoPOS*, logo, telephone `+60182889932`, `contactPoint` (sales, `ms`), areaServed Malaysia.
   - **WebSite** and **WebPage** (`inLanguage: ms-MY`).
   - **Service** "Website Premium Mampu Milik", with an **Offer** of `price: 200`, `priceCurrency: MYR`. The page's package card defines a fixed RM200 package (with inclusions and exclusions), so a fixed price is supported. The description states the exclusions. `priceValidUntil` is left out because no promotion end date is published.
2. `#schema-faq` holds the **FAQPage** with 12 Q&As. It was **generated from the visible FAQ text**, and a script confirmed the two match exactly.

Not used, on purpose: **LocalBusiness** (no verified physical address), and reviews, ratings, awards or client counts (none verified). Note that Google currently shows FAQ rich results only for government and health sites. The markup still helps search and AI systems understand the page.

> ⚠️ Maintenance: if you edit an FAQ answer in the HTML, update the matching text in `#schema-faq` too.

## 5. New content (AEO / GEO)

- **FAQ** expanded from 4 to 12 questions in natural Bahasa Melayu Malaysia. It covers all 10 requested questions. The previous 4 questions were kept or merged, so no information was lost.
- **About section (`#tentang`)** covers who Dyno serves (industries taken from the real portfolio only), the services offered, and why an affordable website makes sense.
- Every answer uses **only facts already on the page**: RM200 promo (original price RM999), the package inclusions and exclusions, a 2-day turnaround after complete materials are received, domain and hosting not included and "dibincangkan berasingan", revisions within an agreed period, no e-commerce, and the 4-step process. The Facebook-vs-website answer and the Google answer are general explanations. The Google answer states clearly that **no one can guarantee page-1 ranking**.
- No testimonials, case studies, reviews or statistics were invented.

## 6. Lead generation (WhatsApp)

- Primary CTA **"Dapatkan Website Premium Bermula RM200"** with the prefilled message *"Saya berminat dengan Website Premium RM200. Boleh berikan maklumat pakej?"* appears in the **hero**, the **services** section (new, under the benefits grid) and the **closing** CTA.
- The **pricing** CTA ("WhatsApp Untuk Tempahan"), the nav CTA and the floating button were kept as they were.
- The WhatsApp number is now a clickable link in the closing section and the footer.
- Each CTA has a `data-cta="hero|services|pricing|closing|nav|footer|floating"` attribute, ready for click tracking. **No tracking was added**, because no analytics was installed. If GA4 or GTM is added later, use these attributes for a "whatsapp_click" event. Also add a cookie/consent notice and update the privacy information (PDPA 2010).

## 7. Crawler accessibility

- `robots.txt` allows every crawler. OAI-SearchBot, ChatGPT-User, PerplexityBot, Googlebot and Bingbot are listed explicitly.
- **AI-training preference unchanged:** GPTBot, Google-Extended and CCBot are not named, so they follow `User-agent: *` (allowed). That matches the site's behaviour before this change, when there was no robots.txt. Opting out of training is the owner's decision.
- There is no `noindex` anywhere.
- GitHub Pages does not block search crawlers. **Not verified:** whether a CDN or firewall (for example Cloudflare "Bot Fight Mode" or "Block AI bots") sits in front of the domain. This sandbox could not reach murahwebsite.my (egress blocked).

## 8. Sitemap, indexing, Bing, IndexNow

- `sitemap.xml` contains the single canonical, indexable URL, with `lastmod`. `robots.txt` references it.
- The Google Search Console property was not touched (it is already verified, per the owner).
- **Bing Webmaster Tools** (manual):
  1. Go to https://www.bing.com/webmasters and sign in.
  2. Choose **Import from Google Search Console**. This is the fastest route and needs no file or meta tag. Alternatively, add `https://murahwebsite.my/` and verify with the XML file, meta tag or DNS option Bing offers. If you use the meta tag, send it over and it can be added to `<head>`.
  3. Submit `https://murahwebsite.my/sitemap.xml` under *Sitemaps*.
  4. Run *URL Inspection* on the homepage.
- **IndexNow (prepared, not submitted):** the key file is `/a83ca945dd5d8e36f8dd2572c5877417.txt`. **After this branch is deployed**, open this URL once in a browser:
  `https://api.indexnow.org/indexnow?url=https://murahwebsite.my/&key=a83ca945dd5d8e36f8dd2572c5877417`
  A `200` or `202` response means the submission was accepted. Repeat only when the page really changes. It is free and needs no paid API.
- Do not assume anything is indexed until Search Console or Bing Webmaster Tools confirms it.

## 9. Tests performed

There is no build or test suite in the repo (static HTML). These checks were run locally:

| Check | Result |
|---|---|
| Exactly one title, description, canonical, robots, viewport and og:title | ✅ |
| No `noindex` | ✅ |
| JSON-LD parses (5 types, no duplicates); FAQ JSON-LD matches the visible FAQ | ✅ |
| One H1, no skipped heading levels, unique ids | ✅ |
| Every `#anchor` link has a target; every image, video and icon file exists | ✅ |
| All 8 WhatsApp links go to `wa.me/60182889932` and the prefilled text decodes correctly | ✅ |
| `robots.txt`, `sitemap.xml`, `llms.txt`, `favicon.ico` and the key file served with HTTP 200 (local server) | ✅ |
| Chromium, desktop 1366 px and iPhone 13: 0 console errors, 0 failed requests, 0 broken images, no horizontal overflow, all `.reveal` content visible | ✅ |
| Before/after screenshots (desktop and mobile) | ✅ Layout, colours and typography unchanged. Visible differences are only the new logo, the edited copy, and the new About, FAQ and CTA content. |
| Nav at 901, 1000, 1180 and 1366 px: no wrapping or overflow | ✅ |
| Live-site checks (real robots.txt, headers, CDN) | ❌ Not possible: the domain is blocked from this sandbox |
| Google Rich Results Test / Schema.org validator | ❌ Not run: external validators are unreachable here. Run them manually after deploy. |

## 10. Outstanding items — please confirm

1. **Brand name.** The site now uses the **Dyno Website Services** logo and "DYNO" wordmark you supplied. The **poster image** at the top of the page still shows the old **DYNOPOS** logo and "www.dynopos.my". Consider a refreshed poster. If you own `dynopos.my` (or social profiles), tell me and I'll add them as `sameAs` in the Organization schema.
2. **Domain and hosting.** The FAQ says these are "dibincangkan secara berasingan", as the page already did. Please confirm the typical cost or arrangement so the FAQ can give a concrete answer.
3. **Promotion terms.** The RM999 "harga asal", "promosi terhad" and the "RM4,000" comparison were kept unchanged. Is there an end date? (It would allow `priceValidUntil`.)
4. **Revision period** ("tempoh dipersetujui") and **payment terms.** These are not stated, so they were not invented.
5. Does the package include any **SEO setup** for clients (for example Search Console submission)? It is not claimed today.
6. Does **018-288 9932** accept phone calls, or WhatsApp only? Only WhatsApp links were used.
7. **Unmerged branch `claude/shrink-pelantar-video`** reduces the autoplay video from 1.1 MB to 216 KB. It is worth merging for mobile speed.
8. The poster's embedded C2PA (content-credential) metadata was dropped when it was converted to JPEG. The original PNG is still in git history if it is needed.
9. Consider a **Google Business Profile** only if the business meets Google's eligibility rules (it needs either a staffed location or a defined service area).

## 11. Deployment

GitHub Pages serves `main`. Nothing in this branch changes the deployment setup. **To go live, merge this branch into `main`** (no pull request has been opened yet). After deploy:

1. Check https://murahwebsite.my/, `/robots.txt` and `/sitemap.xml` in a browser.
2. Run Google's Rich Results Test and validator.schema.org on the homepage.
3. In Search Console, run URL Inspection, then Request Indexing.
4. Set up Bing Webmaster Tools and send the IndexNow ping (§8).
