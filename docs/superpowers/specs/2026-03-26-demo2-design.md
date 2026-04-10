# Demo2 Homepage — First Point Physio (Client Brand)

## Overview

Alternative demo homepage (`demo2.html`) using the client's own brand colours (navy/blue from their brochure PDF), updated content from BrandScript 2, and high-end design principles. This replaces the teal/orange Figtree design with a navy/blue Montserrat/Poppins design that feels more aligned with how First Point Physio presents itself.

## Technical Decisions

- **Single self-contained HTML file** — no external dependencies beyond Google Fonts
- **Fonts:** Montserrat (headings, 700/800) + Poppins (body, 400/500/600) via Google Fonts
- **Colour palette from client brochure:**
  - Dark navy `#041c40` (hero bg, dark sections, off-black)
  - Mid blue `#135ca0` (headings, accents)
  - Bright blue `#3f7bf0` (CTAs, links, single accent)
  - Sky blue `#56aeff` (secondary accents, tags, hover states)
  - Light teal `#b0d4df` (soft backgrounds)
  - Near-navy `#051d40` (body text)
  - White `#ffffff`
- **No pure black anywhere** — darkest value is `#041c40`
- **Tinted shadows** — `rgba(4, 28, 64, 0.08)` instead of generic black
- **Meta:** `noindex, nofollow`, Microsoft Clarity analytics
- **Not linked from index.html** — standalone alternative for now

## Design Principles Applied

- **DESIGN_VARIANCE: 8** — asymmetric hero (split-screen, left-aligned text), no centered heroes, offset grids, generous whitespace
- **MOTION_INTENSITY: 6** — staggered scroll-reveal with IntersectionObserver, CSS cubic-bezier transitions, tactile button feedback, kinetic marquee
- **VISUAL_DENSITY: 4** — airy, art-gallery spacing, large section padding, content breathing room
- **No 3-equal-card rows** — use 2-col zig-zag or asymmetric bento grids
- **Cards only where elevation communicates hierarchy** — stats use oversized typography with border dividers, not card boxes
- **Single accent colour** — bright blue `#3f7bf0` for all CTAs
- **Tactile feedback** — buttons scale down on `:active` with `-translate-y` and `scale(0.98)`

## Page Structure (11 Sections)

### Navigation
- Fixed top, navy background `#041c40`, logo left, nav links right
- Nav items: Services | For PCNs | Results | About | Contact
- CTA button (bright blue): "Get in Touch"
- Mobile burger menu with full-screen navy overlay
- Blur backdrop on scroll for depth

### Section 1: Hero (Split-Screen)
- **Layout:** 2-column asymmetric — text content on left (~55%), image/visual area on right (~45%)
- **Left side:**
  - Small badge/tag: "Managed FCP Services for Primary Care" in sky blue
  - Headline: "Free Up Your GPs. We Handle MSK." — Montserrat 800, clamp(38px, 6vw, 56px), tracking tight, dark navy on light bg OR white on dark bg
  - Sub-headline: "Fully managed First Contact Practitioners for your PCN — recruited, supervised, and covered. Small team. Big impact. Zero hassle." — Poppins 400, muted colour
  - Two CTAs: "Get in Touch" (bright blue solid) + "Download the Case Study" (outline/ghost)
  - Small trust line below: "Trusted by 120+ GP surgeries since 2017"
- **Right side:** Large image area with soft gradient fade into background. Use the existing hero image or a placeholder
- **Background:** Light/warm white, not pure white — something like `#f8f9fc`

### Section 2: Trust Marquee
- Infinite horizontal scrolling band
- Navy background `#041c40`
- Stats in white with sky blue dividers/accents:
  - "Since 2017" | "50+ Clinicians" | "120+ GP Surgeries" | "87% Managed In-Service" | "Fully Funded Within ARRS"
- Duplicated content for seamless infinite loop via CSS animation
- Subtle grain overlay for texture

### Section 3: Stakes / Problem ("Sound Familiar?")
- **Layout:** Left-aligned text block, max-width 65ch
- Light background section
- Heading: "Sound Familiar?" — large, mid blue
- Copy from BrandScript 2: GPs spending 30% on MSK, ARRS funding available but recruitment nightmare, large providers delivering inconsistency, patients waiting
- Tone: empathetic, not aggressive
- Optional: subtle left border accent or pull-quote styling

### Section 4: Value Proposition ("What Changes When You Work With Us")
- **Layout:** 2-column zig-zag (NOT 3 equal cards)
  - Row 1: Icon/number left, text right
  - Row 2: Text left, icon/number right
  - Or: asymmetric 2-col bento grid with varied card sizes
- Four benefits:
  1. **GP Time Reclaimed** — MSK patients seen by specialist, dozens of freed appointments weekly
  2. **ARRS Funding Put to Work** — fully funded within scheme, no wasted budget
  3. **Zero Operational Burden** — recruitment, supervision, cover all managed
  4. **A Partner, Not a Provider** — small team, responsive communication, know your practice by name
- Cards have spotlight border on hover (border illuminates from cursor direction)
- Light teal `#b0d4df` background for this section

### Section 5: Guide ("We Know What It's Like")
- **Layout:** Split — empathy text on one side, authority stats on the other
- **Empathy side:**
  - Heading: "We Know What It's Like"
  - Copy about understanding the pressure, not having to become an MSK staffing agency, wanting a partner who picks up the phone
- **Authority side:**
  - Large stat numbers (oversized Montserrat 800) with labels beneath
  - `87%` managed in-service | `98%` utilisation | `94%` would recommend | `80%` no GP follow-up needed
  - No card boxes — just big numbers, `border-t` dividers, clean typography
- Optional testimonial below in a subtle quote style

### Section 6: 3-Step Plan ("Getting Started Is Simple")
- **Layout:** 3 numbered steps in a horizontal flow with connecting line/arrow between them
- Navy dark background `#041c40` for contrast shift
- White text, sky blue step numbers in circles
- Steps:
  1. **Get in Touch** — tell us about your PCN, no obligation
  2. **We Handle Everything** — recruit, vet, place, supervise, cover
  3. **Your GPs Focus on What Matters** — MSK sorted, GP time back, monthly reporting
- CTA below: "Get in Touch" button (bright blue on dark)

### Section 7: What Sets Us Apart
- **Layout:** 2x2 asymmetric grid (NOT 4 equal cards) — vary card sizes, one larger feature card
- Light background
- Four differentiators from brochure:
  1. **Personalised Service** — small, agile, aligned with your priorities. The director answers his phone.
  2. **Clinical Development** — structured CPD pathways, all clinicians supervised and up to date
  3. **Performance Reporting** — monthly bespoke reports with clinic-level utilisation, outcomes, patient feedback
  4. **Responsive Communication** — solution-focused, same-day resolution, no escalation tiers
- Cards have subtle inner border + tinted shadow, hover lifts with spotlight effect

### Section 8: The Numbers
- **Layout:** Large typographic section — oversized stats with supporting text
- Navy background `#041c40`
- Stats displayed as massive numbers (Montserrat 800, ~72px) in white/sky blue with supporting label beneath
- Key stats: 87% | 98% | 94% | 80% | 50+ | 120+
- No card boxes — pure typography, `border-t` dividers between stat groups or a horizontal scrolling layout
- Source attribution: "From our monthly PCN reports and the National FCP Evaluation"

### Section 9: Service Overview ("Everything Included. One Price.")
- **Layout:** Two-column — checklist on left, ARRS funding callout card on right
- Light background
- Checklist items with checkmark SVGs:
  - Qualified FCP placed in your practice
  - Full recruitment and vetting
  - Clinical supervision and ongoing CPD
  - Holiday and sickness cover as standard
  - Monthly outcome and activity reporting
  - ARRS-funding aligned — one transparent price
  - Flexible engagement — stay because you want to
- Right side: highlighted callout card about ARRS funding being fully refundable

### Section 10: Lead Generator / Case Study CTA
- **Layout:** Distinct background section (navy or gradient)
- Heading: "See the Results for Yourself"
- Sub-text: "Download our case study showing how a PCN freed up GP time and put ARRS funding to work with First Point Physio."
- Bullet points of what they'll see in the case study
- Email capture form: work email field + "Download the Case Study" button
- This feeds into a 6-email nurture sequence (not built here, just the capture form)

### Section 11: Footer
- Navy background `#041c40`
- Final CTA: "Ready to free up your GP appointments? Get in Touch"
- Contact details: info@firstpointphysio.co.uk | Phillip Dale: 07731526103
- Online meeting booking link
- Coverage areas
- Navigation links
- Copyright: First Point Physio Ltd

## Responsive Approach

- **Desktop (1200px+):** Full asymmetric layouts, split screens, multi-column grids
- **Tablet (768-1199px):** Reduce to 2 columns where needed, maintain asymmetry
- **Mobile (<768px):** Single column, full-width, aggressive stacking. All asymmetric layouts collapse to linear flow. CTA buttons full-width. Tap-to-call on phone numbers. Min 44px touch targets.

## Animation / Motion

- **Scroll reveal:** IntersectionObserver with `threshold: 0.08`, staggered `animation-delay` via CSS custom properties
- **Easing:** `cubic-bezier(0.16, 1, 0.3, 1)` for all transitions
- **Marquee:** CSS `@keyframes` infinite scroll, `animation: marquee 30s linear infinite`
- **Button feedback:** `:active { transform: translateY(1px) scale(0.98) }`
- **Hover states:** `transform: translateY(-4px)` with tinted `box-shadow`
- **Reduced motion:** `@media (prefers-reduced-motion: reduce)` disables all animations

## Print Styles

- Hide nav, marquee, grain overlay
- Single column layout
- Dark backgrounds convert to light for ink saving
- `break-inside: avoid` on content blocks
