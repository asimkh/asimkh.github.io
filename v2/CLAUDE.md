# CLAUDE.md — Slicky Ads / Asim Khan marketing site

Project context for future sessions. Read this before working on the site.

## What this is

A static marketing site for **Asim Khan** — a Dubai-based Marketing Operations Manager / AI Growth Operator trading as **Slicky Ads**. Hand-authored HTML/CSS/JS, no build step, no framework. Deployed on **GitHub Pages** with a custom domain.

- Custom domain (canonical): **slickyads.com**
- Repo origin: asimkh.github.io (Pages)
- GTM container: `GTM-MFPL72SN` (on all main pages)
- Phone / WhatsApp: +971 54 359 9147 → `https://wa.me/971543599147`
- Lead capture: client-side JS composes a pre-filled WhatsApp message (no form backend)

## Structure

```
v2/
  index.html          Home (hero + lead form + services explorer)
  services.html       Service details
  case-studies.html   Case studies
  work.html           Portfolio (DTC brand work + work/work-details.html)
  blog.html           Medium blog pull
  contact.html        Contact form (WhatsApp submit)
  privacy.html
  terms.html
  sitemap.xml         → slickyads.com URLs
  robots.txt          → points to sitemap.xml (added 2026-09-04)
  assets/
    slickyads_logo.png   nav logo
    slickyads_logo1.png  footer logo (different — reconcile?)
    profile/ak_profile_img.png   founder photo (also used as OG image)
    favicon/site.webmanifest    web manifest (needs fixes — see TODO)
    ecommerce/ google-ads/ lead-generation/ meta-ads/   service imagery
  ../v1/   older version of the site (reference only, not deployed)
  ../_private/   gitignored private assets
```

Pages are large single files (~500–850 lines) with an inline `<style>` design system (CSS custom properties: `--primary` #2438C7, `--coral` #FF6A4D, `--teal` #0F9D8E, etc.). Fonts: Space Grotesk (display), Inter (body), IBM Plex Mono (mono). Nav links use extensionless paths (e.g. `href="services"`).

## Conventions

- Keep it dependency-free: no npm, no build. Inline CSS/JS only.
- Match the existing design system — use the CSS variables, not hardcoded colors.
- Extensionless internal links (GitHub Pages serves the .html).
- Every page shares the same `<header class="nav">` and `<footer>` block; keep them consistent across pages when editing one.
- `.DS_Store` is gitignored; but tracked copies in some asset dirs still need `git rm --cached`.

## Deploy

Push to `master` on the asimkh.github.io repo → GitHub Pages serves `v2/` (via CNAME = `slickyads.com`). No CI.

## SEO state (as of 2026-09-04)

Done this session:
- Added `robots.txt` (allows all, points to sitemap).
- Added `<link rel="canonical">` to all 8 pages → `https://slickyads.com/<page>`.
- Aligned all `og:url` to `slickyads.com` (was `asimkh.github.io`).
- Added full Open Graph + Twitter card blocks to the 5 pages that had none (services, case-studies, blog, contact, work).
- Repointed OG/Twitter image from a missing file (`assets/profile/asimkh-marketing-expert.png`) to the existing `assets/profile/ak_profile_img.png` on slickyads.com. Removed the wrong `og:image:width/height` (1200×630) that matched the missing file.

## Remaining review items (prioritized)

From a site review done 2026-09-04. Items 1 & 2 are now done.

1. ✅ Fix missing OG image + web manifest icon paths.
2. ✅ robots.txt + canonical + align OG URLs to slickyads.com.
3. **Add `LocalBusiness` / `ProfessionalService` JSON-LD** structured data (address Aspin Tower Dubai, phone, services). Not done yet.
4. **Fix web manifest**: `"name":"MyWebSite"`/`"short_name":"MySite"` → "Asim Khan" / "Slicky Ads"; manifest icon paths point to `/web-app-manifest-*.png` at root but files live at `assets/favicon/`. Not done.
5. **Revisit References section** on home — testimonials are written in third person ("David has worked directly with Asim…") rather than as actual quotes. Feels like placeholder copy. Not done.
6. **`work.html` inconsistencies**: `<title>` says "Case Studies", nav highlights "Case Studies" (Portfolio isn't in nav, only footer). OG title was set to "Portfolio" in this session — title + nav should be reconciled. Not done.
7. **Two logos** (`slickyads_logo.png` nav vs `slickyads_logo1.png` footer) — intentional? Not done.
8. **Contact form has no fallback** if user lacks WhatsApp (it just composes a wa.me URL). Consider `mailto:` fallback. Not done.
9. `git rm --cached` the tracked `.DS_Store` files. Not done.

## Notes

- `v1/` is the previous design; don't edit unless asked.
- `_private/` is gitignored.
- The site is light and accessible (prefers-reduced-motion, focus-visible, alt text). Preserve that.
