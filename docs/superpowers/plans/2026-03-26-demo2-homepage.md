# Demo2 Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build an alternative demo homepage (`demo2.html`) for First Point Physio using the client's navy/blue brand palette, BrandScript 2 content, and high-end design principles.

**Architecture:** Single self-contained HTML file with inline CSS and vanilla JavaScript. Split-screen asymmetric hero, staggered scroll-reveal animations via IntersectionObserver, kinetic trust marquee, oversized typographic stats section, and responsive mobile-first design. Navy/blue colour palette from the client's brochure PDF.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, clamp, keyframe animations), vanilla JavaScript, Google Fonts (Montserrat + Poppins)

**Reference files:**
- Design spec: `docs/superpowers/specs/2026-03-26-demo2-design.md`
- Content source: `projectcontext/brandscript2.md`
- Client brochure (colour/content reference): `projectcontext/First Point Physio Brochure .pdf`
- Existing demo for structural reference: `demo.html`

**Design taste directives applied:**
- DESIGN_VARIANCE: 8 — asymmetric layouts, split-screen hero, no centered heroes, no 3-equal-card rows
- MOTION_INTENSITY: 6 — staggered scroll-reveal, CSS cubic-bezier transitions, tactile button feedback, kinetic marquee
- VISUAL_DENSITY: 4 — airy spacing, generous padding, content breathing room
- No pure black — darkest is `#041c40`
- Tinted shadows — `rgba(4, 28, 64, 0.08)`
- Single accent colour — `#3f7bf0`
- Tactile button `:active` feedback

---

### Task 1: Create demo2.html with head, CSS design system, and navigation

**Files:**
- Create: `demo2.html`

- [ ] **Step 1: Create the file with full `<head>` and CSS custom properties**

Create `demo2.html` with:
- Clarity analytics script (copy from `demo.html` lines 4-9)
- Meta tags: charset UTF-8, viewport, `noindex nofollow`, title "First Point Physio — Managed FCP Services for Primary Care"
- Meta description: "Fully managed First Contact Practitioners for your PCN. 50+ clinicians, 120+ GP surgeries, since 2017. Small team. Big impact. Zero hassle."
- Google Fonts: `https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800;900&family=Poppins:wght@300;400;500;600;700&display=swap`

CSS `:root` variables:

```css
:root {
  --navy: #041c40;
  --navy-90: rgba(4, 28, 64, 0.9);
  --navy-light: #0a2a54;
  --blue: #135ca0;
  --blue-bright: #3f7bf0;
  --blue-bright-hover: #2d6ae0;
  --blue-bright-glow: rgba(63, 123, 240, 0.25);
  --sky: #56aeff;
  --sky-light: rgba(86, 174, 255, 0.12);
  --teal-bg: #b0d4df;
  --teal-bg-light: rgba(176, 212, 223, 0.15);
  --teal-bg-soft: #e8f2f6;
  --bg: #f8f9fc;
  --bg-warm: #f4f6fa;
  --white: #ffffff;
  --text: #051d40;
  --text-2: #2a3f5f;
  --text-muted: #5a6d85;
  --text-light: #8a9bb0;
  --border: #d8e0ea;
  --border-light: #e8edf4;
  --shadow: rgba(4, 28, 64, 0.08);
  --shadow-lg: rgba(4, 28, 64, 0.12);
  --heading: 'Montserrat', system-ui, sans-serif;
  --body: 'Poppins', system-ui, sans-serif;
  --r-sm: 8px;
  --r-md: 12px;
  --r-lg: 16px;
  --r-xl: 24px;
  --r-2xl: 32px;
  --r-full: 100px;
  --ease: cubic-bezier(0.16, 1, 0.3, 1);
}
```

Base reset and body styles:

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; scroll-padding-top: 80px; }
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}
body {
  font-family: var(--body); font-size: 16px; line-height: 1.75;
  color: var(--text); background: var(--bg);
  overflow-x: hidden; -webkit-font-smoothing: antialiased;
}
img { max-width: 100%; height: auto; display: block; }
a { color: inherit; text-decoration: none; }
button { font-family: inherit; cursor: pointer; border: none; background: none; }
ul { list-style: none; }
h1,h2,h3,h4,h5,h6 { font-family: var(--heading); font-weight: 700; line-height: 1.15; color: var(--text); }
.sr-only { position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px; overflow: hidden; clip: rect(0,0,0,0); border: 0; }
.container { width: 100%; max-width: 1200px; margin: 0 auto; padding: 0 24px; }
```

Button styles:

```css
.btn {
  position: relative; display: inline-flex; align-items: center; justify-content: center; gap: 10px;
  padding: 16px 36px; font-family: var(--heading); font-size: 15px; font-weight: 700;
  line-height: 1; border-radius: var(--r-full); transition: all 0.35s var(--ease);
  cursor: pointer; min-height: 52px; white-space: nowrap; letter-spacing: 0.01em;
}
.btn svg { transition: transform 0.3s var(--ease); flex-shrink: 0; }
.btn:hover svg { transform: translateX(3px); }
.btn:active { transform: translateY(1px) scale(0.98); }
.btn:focus-visible { outline: 3px solid var(--blue-bright); outline-offset: 3px; }

.btn-primary {
  background: var(--blue-bright); color: var(--white);
  box-shadow: 0 4px 15px var(--blue-bright-glow), inset 0 1px 0 rgba(255,255,255,0.15);
  border: 1px solid rgba(255,255,255,0.1);
}
.btn-primary:hover {
  background: var(--blue-bright-hover); transform: translateY(-2px);
  box-shadow: 0 8px 25px var(--blue-bright-glow), inset 0 1px 0 rgba(255,255,255,0.15);
}

.btn-outline {
  color: var(--text); border: 2px solid var(--border);
  background: var(--white); box-shadow: 0 2px 8px var(--shadow);
}
.btn-outline:hover { border-color: var(--blue); color: var(--blue); transform: translateY(-2px); box-shadow: 0 4px 16px var(--shadow); }

.btn-outline-light {
  color: var(--white); border: 2px solid rgba(255,255,255,0.25);
  background: rgba(255,255,255,0.05);
}
.btn-outline-light:hover { background: rgba(255,255,255,0.12); border-color: rgba(255,255,255,0.5); transform: translateY(-2px); }

.btn-sm { padding: 12px 24px; font-size: 13.5px; min-height: 44px; }
```

Scroll reveal styles:

```css
.reveal { opacity: 0; transform: translateY(40px); }
.reveal.vis { opacity: 1; transform: translateY(0); transition: opacity 0.8s var(--ease), transform 0.8s var(--ease); }
.d1 { transition-delay: 0.08s !important; }
.d2 { transition-delay: 0.16s !important; }
.d3 { transition-delay: 0.24s !important; }
.d4 { transition-delay: 0.32s !important; }
```

Section utility:

```css
.section { padding: 120px 0; position: relative; }
.section-sm { padding: 80px 0; }
.section--navy { background: var(--navy); color: var(--white); }
.section--teal { background: var(--teal-bg-soft); }
.section--warm { background: var(--bg-warm); }

.badge {
  display: inline-flex; align-items: center; gap: 8px; padding: 8px 20px;
  background: var(--sky-light); border: 1px solid rgba(86,174,255,0.2);
  border-radius: var(--r-full); font-family: var(--heading); font-size: 13px; font-weight: 700;
  color: var(--blue); letter-spacing: 0.04em; text-transform: uppercase;
}
.badge-dark { background: rgba(255,255,255,0.06); border-color: rgba(255,255,255,0.1); color: var(--sky); }
```

Grain overlay:

```css
.grain { position: fixed; inset: 0; pointer-events: none; z-index: 9998; opacity: 0.02; mix-blend-mode: multiply; }
```

- [ ] **Step 2: Add navigation CSS**

```css
/* ═══ NAVIGATION ═══ */
.nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
  background: rgba(4, 28, 64, 0.95); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255,255,255,0.06);
  transition: all 0.4s var(--ease);
}
.nav-inner {
  display: flex; align-items: center; justify-content: space-between; padding: 16px 0;
}
.nav-logo { height: 34px; width: auto; }
.nav-links { display: flex; align-items: center; gap: 4px; }
.nav-link {
  padding: 10px 16px; font-family: var(--heading); font-size: 14px; font-weight: 600;
  color: rgba(255,255,255,0.6); border-radius: var(--r-sm); transition: all 0.25s var(--ease);
}
.nav-link:hover { color: var(--white); }
.nav-link:focus-visible { outline: 2px solid var(--sky); outline-offset: 2px; }
.nav-cta { margin-left: 12px; }

.burger {
  display: none; flex-direction: column; gap: 6px; padding: 10px; cursor: pointer; z-index: 1010;
}
.burger span {
  display: block; width: 26px; height: 2px; background: var(--white);
  border-radius: 4px; transition: all 0.35s var(--ease); transform-origin: center;
}
.burger.active span:nth-child(1) { transform: rotate(45deg) translate(6px, 6px); }
.burger.active span:nth-child(2) { opacity: 0; transform: scaleX(0); }
.burger.active span:nth-child(3) { transform: rotate(-45deg) translate(6px, -6px); }

.mobile-nav {
  position: fixed; inset: 0; background: var(--navy); z-index: 1005;
  display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 10px;
  opacity: 0; pointer-events: none; transition: opacity 0.35s var(--ease);
}
.mobile-nav.open { opacity: 1; pointer-events: auto; }
.mobile-nav .nav-link { font-size: 20px; padding: 14px 24px; color: var(--white); }
.mobile-nav .btn { margin-top: 20px; width: 80%; max-width: 320px; }
.mobile-nav .mobile-contact {
  margin-top: 24px; display: flex; flex-direction: column; gap: 12px; align-items: center;
}
.mobile-nav .mobile-contact a {
  font-size: 15px; color: rgba(255,255,255,0.5); display: flex; align-items: center; gap: 8px; transition: color 0.2s;
}
.mobile-nav .mobile-contact a:hover { color: var(--sky); }
.mobile-nav .mobile-contact a svg { width: 16px; height: 16px; stroke: currentColor; }
```

- [ ] **Step 3: Add navigation HTML**

```html
<body>
  <svg class="grain" aria-hidden="true"><filter id="g"><feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="4" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(#g)"/></svg>

  <header class="nav" id="nav">
    <div class="container">
      <div class="nav-inner">
        <a href="#" aria-label="First Point Physio — Home">
          <img src="images/logo (1).jpg" alt="First Point Physio" class="nav-logo" width="150" height="34">
        </a>
        <nav class="nav-links" aria-label="Main navigation">
          <a href="#benefits" class="nav-link">Services</a>
          <a href="#apart" class="nav-link">Why Us</a>
          <a href="#numbers" class="nav-link">Results</a>
          <a href="#service" class="nav-link">What's Included</a>
        </nav>
        <div class="nav-cta">
          <a href="#footer-cta" class="btn btn-primary btn-sm">Get in Touch</a>
        </div>
        <button class="burger" id="burger" aria-label="Open menu" aria-expanded="false">
          <span></span><span></span><span></span>
        </button>
      </div>
    </div>
    <nav class="mobile-nav" id="mobileNav" role="dialog" aria-label="Mobile navigation">
      <a href="#benefits" class="nav-link">Services</a>
      <a href="#apart" class="nav-link">Why Us</a>
      <a href="#numbers" class="nav-link">Results</a>
      <a href="#service" class="nav-link">What's Included</a>
      <a href="#footer-cta" class="btn btn-primary">Get in Touch</a>
      <div class="mobile-contact">
        <a href="mailto:info@firstpointphysio.co.uk"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg> info@firstpointphysio.co.uk</a>
        <a href="tel:+447731526103"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg> 07731 526 103</a>
      </div>
    </nav>
  </header>

  <!-- Sections go here -->

</body>
```

Add responsive nav rules inside a `@media (max-width: 900px)` block:

```css
@media (max-width: 900px) {
  .nav-links, .nav-cta { display: none; }
  .burger { display: flex; }
}
```

- [ ] **Step 4: Add JavaScript before `</body>`**

Mobile menu toggle, scroll reveal (IntersectionObserver), and smooth scroll:

```html
<script>
(function() {
  'use strict';
  var prefersRM = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  // Mobile menu
  var burger = document.getElementById('burger');
  var mobileNav = document.getElementById('mobileNav');
  burger.addEventListener('click', function() {
    var open = mobileNav.classList.contains('open');
    mobileNav.classList.toggle('open');
    burger.classList.toggle('active');
    burger.setAttribute('aria-expanded', open ? 'false' : 'true');
    document.body.style.overflow = open ? '' : 'hidden';
  });
  mobileNav.querySelectorAll('a').forEach(function(a) {
    a.addEventListener('click', function() {
      mobileNav.classList.remove('open');
      burger.classList.remove('active');
      burger.setAttribute('aria-expanded', 'false');
      document.body.style.overflow = '';
    });
  });

  // Scroll reveal
  var reveals = document.querySelectorAll('.reveal');
  if (prefersRM) {
    reveals.forEach(function(el) { el.classList.add('vis'); });
  } else {
    var obs = new IntersectionObserver(function(entries) {
      entries.forEach(function(e) {
        if (e.isIntersecting) { e.target.classList.add('vis'); obs.unobserve(e.target); }
      });
    }, { threshold: 0.08, rootMargin: '0px 0px -30px 0px' });
    reveals.forEach(function(el) { obs.observe(el); });
  }

  // Smooth scroll
  document.querySelectorAll('a[href^="#"]').forEach(function(a) {
    a.addEventListener('click', function(e) {
      var id = this.getAttribute('href');
      if (id === '#') return;
      var target = document.querySelector(id);
      if (target) {
        e.preventDefault();
        var top = target.getBoundingClientRect().top + window.pageYOffset - 80;
        window.scrollTo({ top: top, behavior: prefersRM ? 'auto' : 'smooth' });
      }
    });
  });
})();
</script>
```

- [ ] **Step 5: Verify and commit**

Open in browser. Check: nav renders on navy background, burger works on mobile, no console errors.

```bash
git add demo2.html
git commit -m "Add demo2.html boilerplate with design system and navigation"
```

---

### Task 2: Add Hero section (split-screen) and Trust Marquee

**Files:**
- Modify: `demo2.html`

- [ ] **Step 1: Add hero CSS**

Add after the navigation CSS:

```css
/* ═══ HERO (Split Screen) ═══ */
.hero {
  min-height: 100dvh; display: flex; align-items: center;
  padding: 120px 0 80px; background: var(--bg); position: relative; overflow: hidden;
}
.hero::after {
  content: ''; position: absolute; top: -200px; right: -100px; width: 600px; height: 600px;
  border-radius: 50%; background: radial-gradient(circle, rgba(19,92,160,0.06), transparent 65%);
  pointer-events: none;
}
.hero-grid {
  display: grid; grid-template-columns: 1fr 0.85fr; gap: 64px; align-items: center;
}
.hero-content { position: relative; z-index: 2; }
.hero-badge { margin-bottom: 28px; }
.hero h1 {
  font-size: clamp(36px, 5.5vw, 56px); font-weight: 800; letter-spacing: -0.035em;
  line-height: 1.08; margin-bottom: 24px; color: var(--navy);
}
.hero h1 em { font-style: normal; color: var(--blue); }
.hero-sub {
  font-size: clamp(16px, 1.8vw, 18px); line-height: 1.75; color: var(--text-muted);
  max-width: 520px; margin-bottom: 40px;
}
.hero-ctas { display: flex; flex-wrap: wrap; gap: 16px; margin-bottom: 32px; }
.hero-trust {
  font-size: 13px; color: var(--text-light); font-family: var(--heading); font-weight: 500;
  display: flex; align-items: center; gap: 8px;
}
.hero-trust svg { width: 16px; height: 16px; stroke: var(--blue); }

.hero-visual {
  position: relative; border-radius: var(--r-2xl); overflow: hidden;
  aspect-ratio: 4/3; background: linear-gradient(135deg, var(--teal-bg-soft), var(--bg-warm));
}
.hero-visual img { width: 100%; height: 100%; object-fit: cover; }
.hero-visual::after {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(135deg, rgba(248,249,252,0.3), transparent 60%);
  pointer-events: none;
}

@media (max-width: 900px) {
  .hero { min-height: auto; padding: 120px 0 60px; }
  .hero-grid { grid-template-columns: 1fr; gap: 40px; }
  .hero-content { text-align: left; }
  .hero-ctas { flex-direction: column; }
  .hero-ctas .btn { width: 100%; max-width: 360px; }
  .hero-visual { max-height: 400px; }
}
@media (max-width: 640px) {
  .hero { padding: 100px 0 48px; }
  .hero-sub { font-size: 15px; }
}
```

- [ ] **Step 2: Add hero HTML**

Insert after `<!-- Sections go here -->`:

```html
<!-- ═══ HERO ═══ -->
<section class="hero" id="hero">
  <div class="container">
    <div class="hero-grid">
      <div class="hero-content">
        <div class="badge hero-badge reveal">Managed FCP Services for Primary Care</div>
        <h1 class="reveal d1">Free Up Your GPs.<br>We Handle <em>MSK</em>.</h1>
        <p class="hero-sub reveal d2">Fully managed First Contact Practitioners for your PCN — recruited, supervised, and covered. Small team. Big impact. Zero hassle.</p>
        <div class="hero-ctas reveal d3">
          <a href="#footer-cta" class="btn btn-primary">
            Get in Touch
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
          </a>
          <a href="#case-study" class="btn btn-outline">
            Download the Case Study
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
          </a>
        </div>
        <div class="hero-trust reveal d4">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
          Trusted by 120+ GP surgeries since 2017
        </div>
      </div>
      <div class="hero-visual reveal d2">
        <img src="images/hero-image-healthy-female-runner.webp" alt="Physiotherapist consulting with a patient in a GP practice" width="600" height="450">
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Add marquee CSS**

```css
/* ═══ TRUST MARQUEE ═══ */
.marquee {
  background: var(--navy); padding: 18px 0; overflow: hidden; position: relative;
  border-top: 1px solid rgba(255,255,255,0.06);
  border-bottom: 1px solid rgba(255,255,255,0.06);
}
.marquee-track {
  display: flex; gap: 48px; width: max-content;
  animation: marquee 35s linear infinite;
}
.marquee-item {
  display: flex; align-items: center; gap: 10px; white-space: nowrap;
  font-family: var(--heading); font-size: 14px; font-weight: 600; color: rgba(255,255,255,0.7);
  letter-spacing: 0.02em;
}
.marquee-item svg { width: 18px; height: 18px; stroke: var(--sky); flex-shrink: 0; }
.marquee-divider { color: rgba(255,255,255,0.15); font-size: 18px; }

@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
```

- [ ] **Step 4: Add marquee HTML**

Insert after the hero closing `</section>`:

```html
<!-- ═══ TRUST MARQUEE ═══ -->
<div class="marquee" aria-hidden="true">
  <div class="marquee-track">
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg> Since 2017</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg> 50+ Clinicians</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg> 120+ GP Surgeries</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg> 87% Managed In-Service</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg> Fully Funded Within ARRS</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg> Since 2017</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg> 50+ Clinicians</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg> 120+ GP Surgeries</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg> 87% Managed In-Service</span>
    <span class="marquee-divider">/</span>
    <span class="marquee-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg> Fully Funded Within ARRS</span>
    <span class="marquee-divider">/</span>
  </div>
</div>
```

- [ ] **Step 5: Verify and commit**

Check: split-screen hero renders, headline left-aligned, image right, marquee scrolls infinitely, responsive stacking on mobile.

```bash
git add demo2.html
git commit -m "Add split-screen hero and trust marquee"
```

---

### Task 3: Add Stakes, Value Proposition, and Guide sections

**Files:**
- Modify: `demo2.html`

- [ ] **Step 1: Add CSS for stakes, benefits grid, and guide section**

```css
/* ═══ STAKES ═══ */
.stakes-content { max-width: 680px; }
.stakes-content h2 {
  font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em;
  color: var(--navy); margin-bottom: 24px;
}
.stakes-content p { font-size: 17px; line-height: 1.85; color: var(--text-2); margin-bottom: 20px; }
.stakes-content p:last-child { margin-bottom: 0; }

/* ═══ BENEFITS ═══ */
.benefits-header { max-width: 600px; margin-bottom: 64px; }
.benefits-header h2 {
  font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em;
  color: var(--navy); margin-bottom: 16px;
}
.benefits-header p { font-size: 17px; color: var(--text-muted); line-height: 1.75; }

.benefits-grid { display: grid; grid-template-columns: 1.2fr 0.8fr; gap: 24px; }
.benefits-grid > :nth-child(2) { grid-row: 1 / 3; }

.benefit-card {
  padding: 40px 32px; background: var(--white);
  border: 1px solid var(--border-light); border-radius: var(--r-xl);
  transition: all 0.4s var(--ease); position: relative; overflow: hidden;
}
.benefit-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  background: linear-gradient(90deg, var(--blue), var(--sky));
  transform: scaleX(0); transition: transform 0.4s var(--ease); transform-origin: left;
}
.benefit-card:hover {
  border-color: transparent; transform: translateY(-4px);
  box-shadow: 0 20px 48px var(--shadow-lg);
}
.benefit-card:hover::before { transform: scaleX(1); }

.benefit-icon {
  width: 52px; height: 52px; border-radius: var(--r-lg);
  display: flex; align-items: center; justify-content: center; margin-bottom: 24px;
}
.benefit-icon svg { width: 26px; height: 26px; stroke-width: 1.8; }
.bi-1 { background: rgba(19,92,160,0.08); } .bi-1 svg { stroke: var(--blue); }
.bi-2 { background: rgba(63,123,240,0.08); } .bi-2 svg { stroke: var(--blue-bright); }
.bi-3 { background: rgba(86,174,255,0.08); } .bi-3 svg { stroke: var(--sky); }
.bi-4 { background: rgba(176,212,223,0.2); } .bi-4 svg { stroke: var(--blue); }

.benefit-card h3 { font-size: 20px; font-weight: 700; margin-bottom: 12px; letter-spacing: -0.01em; }
.benefit-card p { font-size: 15px; line-height: 1.7; color: var(--text-2); }

@media (max-width: 900px) {
  .benefits-grid { grid-template-columns: 1fr; }
  .benefits-grid > :nth-child(2) { grid-row: auto; }
}
@media (max-width: 640px) {
  .benefit-card { padding: 28px 24px; }
}

/* ═══ GUIDE ═══ */
.guide-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 64px; align-items: start; }
.guide-empathy h2 {
  font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em;
  color: var(--navy); margin-bottom: 24px;
}
.guide-empathy p { font-size: 17px; line-height: 1.85; color: var(--text-2); margin-bottom: 20px; }

.guide-stats { display: grid; grid-template-columns: 1fr 1fr; gap: 0; }
.guide-stat {
  padding: 28px 24px; border-top: 2px solid var(--border-light);
}
.guide-stat:nth-child(odd) { border-right: 2px solid var(--border-light); }
.guide-stat-num {
  font-family: var(--heading); font-size: clamp(36px, 5vw, 52px); font-weight: 800;
  color: var(--blue); line-height: 1; margin-bottom: 8px; letter-spacing: -0.03em;
}
.guide-stat-label { font-size: 14px; color: var(--text-muted); line-height: 1.5; font-weight: 500; }

@media (max-width: 900px) {
  .guide-grid { grid-template-columns: 1fr; gap: 40px; }
}
```

- [ ] **Step 2: Add stakes HTML**

Insert after the marquee:

```html
<!-- ═══ STAKES ═══ -->
<section class="section" id="stakes">
  <div class="container">
    <div class="stakes-content">
      <div class="badge reveal" style="margin-bottom: 20px;">The Challenge</div>
      <h2 class="reveal d1">Sound Familiar?</h2>
      <p class="reveal d2">Your GPs are spending up to a third of their day on musculoskeletal cases they shouldn't need to see. You know ARRS funding could pay for a First Contact Practitioner — but recruiting one is a nightmare. The last time you tried, the role sat empty for months.</p>
      <p class="reveal d3">When you did find someone through a large provider, you got rotating clinicians, impersonal account management, and issues that took weeks to resolve. Meanwhile, patients wait longer, GPs burn out faster, and funding that should be transforming your service sits unused.</p>
      <p class="reveal d4">You don't need another faceless provider. You need a partner who knows your practice by name.</p>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Add benefits HTML**

```html
<!-- ═══ BENEFITS ═══ -->
<section class="section section--teal" id="benefits">
  <div class="container">
    <div class="benefits-header reveal">
      <div class="badge" style="margin-bottom: 20px;">The Difference</div>
      <h2>What Changes When You Work With Us</h2>
    </div>

    <div class="benefits-grid">
      <div class="benefit-card reveal d1">
        <div class="benefit-icon bi-1">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
        </div>
        <h3>GP Time Reclaimed</h3>
        <p>MSK patients are seen by a specialist physiotherapist, not your GPs. That means dozens of freed-up appointments every week for complex patients who actually need a doctor.</p>
      </div>

      <div class="benefit-card reveal d2" style="display:flex;flex-direction:column;justify-content:center;">
        <div class="benefit-icon bi-2">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg>
        </div>
        <h3>ARRS Funding Put to Work</h3>
        <p>Your FCP is fully funded through ARRS. We help you make the most of your allocation — no wasted budget, no clawback risk. The service cost is completely refundable within the scheme.</p>
      </div>

      <div class="benefit-card reveal d3">
        <div class="benefit-icon bi-3">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
        </div>
        <h3>Zero Operational Burden</h3>
        <p>We recruit, supervise, train, and provide cover. You don't manage rotas, chase locums, or handle HR. It's fully managed — that's the whole point.</p>
      </div>

      <div class="benefit-card reveal d4" style="grid-column: 1 / -1;">
        <div class="benefit-icon bi-4">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
        </div>
        <h3>A Partner, Not a Provider</h3>
        <p>We're a small, agile team. The director answers his phone. We know your practice by name. Issues get resolved the same day, not escalated through three tiers of account management. That's the difference between a partner and a provider.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Add guide HTML**

```html
<!-- ═══ GUIDE ═══ -->
<section class="section" id="guide">
  <div class="container">
    <div class="guide-grid">
      <div class="guide-empathy reveal">
        <div class="badge" style="margin-bottom: 20px;">Your Partner</div>
        <h2>We Know What It's Like</h2>
        <p>Running a PCN means balancing clinical quality, operational demands, and funding requirements — often with a team that's already stretched. Adding FCP recruitment to that list shouldn't feel like another full-time job.</p>
        <p>We built First Point Physio because we believe practices deserve a partner who genuinely takes the burden off — not one who adds to it. We've been doing this since 2017, and we're still small enough to care about every practice we work with.</p>
      </div>
      <div class="guide-stats reveal d2">
        <div class="guide-stat">
          <div class="guide-stat-num">87%</div>
          <div class="guide-stat-label">of patients managed within the service — no onward referral needed</div>
        </div>
        <div class="guide-stat">
          <div class="guide-stat-num">98%</div>
          <div class="guide-stat-label">appointment utilisation rate across all clinics</div>
        </div>
        <div class="guide-stat">
          <div class="guide-stat-num">94%</div>
          <div class="guide-stat-label">of patients would recommend the FCP service to others</div>
        </div>
        <div class="guide-stat">
          <div class="guide-stat-num">80%</div>
          <div class="guide-stat-label">didn't need to visit their GP for the same problem again</div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 5: Verify and commit**

Check: stakes section left-aligned, benefit cards in asymmetric grid, guide section split with oversized stat numbers. Mobile: all stack to single column.

```bash
git add demo2.html
git commit -m "Add stakes, benefits, and guide sections"
```

---

### Task 4: Add Plan, What Sets Us Apart, and Numbers sections

**Files:**
- Modify: `demo2.html`

- [ ] **Step 1: Add CSS for plan, differentiators, and numbers**

```css
/* ═══ 3-STEP PLAN ═══ */
.plan-header { text-align: center; max-width: 600px; margin: 0 auto 64px; }
.plan-header h2 { color: var(--white); font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em; margin-bottom: 16px; }
.plan-header p { font-size: 17px; line-height: 1.75; color: rgba(255,255,255,0.55); }

.plan-steps { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; margin-bottom: 48px; }
.plan-step {
  background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08);
  border-radius: var(--r-xl); padding: 40px 28px; text-align: center;
  transition: all 0.4s var(--ease);
}
.plan-step:hover { background: rgba(255,255,255,0.07); transform: translateY(-4px); border-color: rgba(86,174,255,0.25); }
.plan-step-num {
  width: 52px; height: 52px; margin: 0 auto 24px; border-radius: 50%;
  background: linear-gradient(135deg, var(--blue), var(--blue-bright));
  display: flex; align-items: center; justify-content: center;
  font-family: var(--heading); font-size: 20px; font-weight: 900; color: var(--white);
  box-shadow: 0 4px 20px rgba(19,92,160,0.4);
}
.plan-step h3 { color: var(--white); font-size: 19px; margin-bottom: 12px; letter-spacing: -0.01em; }
.plan-step p { font-size: 15px; line-height: 1.75; color: rgba(255,255,255,0.5); }

.plan-cta { text-align: center; }

@media (max-width: 900px) {
  .plan-steps { grid-template-columns: 1fr; max-width: 480px; margin: 0 auto 48px; }
}

/* ═══ WHAT SETS US APART ═══ */
.apart-header { max-width: 600px; margin-bottom: 64px; }
.apart-header h2 { font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em; margin-bottom: 16px; }
.apart-header p { font-size: 17px; color: var(--text-muted); line-height: 1.75; }

.apart-grid { display: grid; grid-template-columns: 1.4fr 0.6fr; grid-template-rows: auto auto; gap: 24px; }
.apart-grid > :first-child { grid-row: 1 / 3; }

.apart-card {
  padding: 36px 28px; background: var(--white);
  border: 1px solid var(--border-light); border-radius: var(--r-xl);
  transition: all 0.4s var(--ease);
}
.apart-card:hover {
  border-color: var(--blue); transform: translateY(-3px);
  box-shadow: 0 16px 40px var(--shadow);
}
.apart-card h3 { font-size: 18px; font-weight: 700; margin-bottom: 12px; letter-spacing: -0.01em; }
.apart-card p { font-size: 15px; line-height: 1.7; color: var(--text-2); }
.apart-card-icon {
  width: 44px; height: 44px; border-radius: var(--r-md);
  display: flex; align-items: center; justify-content: center; margin-bottom: 20px;
  background: var(--sky-light);
}
.apart-card-icon svg { width: 22px; height: 22px; stroke: var(--blue); stroke-width: 1.8; }

@media (max-width: 900px) {
  .apart-grid { grid-template-columns: 1fr; }
  .apart-grid > :first-child { grid-row: auto; }
}

/* ═══ THE NUMBERS ═══ */
.numbers-header { text-align: center; max-width: 600px; margin: 0 auto 72px; }
.numbers-header h2 { color: var(--white); font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em; margin-bottom: 16px; }
.numbers-header p { font-size: 17px; line-height: 1.75; color: rgba(255,255,255,0.5); }

.numbers-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0; }
.number-item {
  padding: 40px 32px; text-align: center;
  border-right: 1px solid rgba(255,255,255,0.08);
  border-bottom: 1px solid rgba(255,255,255,0.08);
}
.number-item:nth-child(3n) { border-right: none; }
.number-item:nth-last-child(-n+3) { border-bottom: none; }
.number-val {
  font-family: var(--heading); font-size: clamp(44px, 6vw, 72px); font-weight: 800;
  color: var(--white); line-height: 1; margin-bottom: 12px; letter-spacing: -0.03em;
}
.number-val span { color: var(--sky); }
.number-label { font-size: 14px; color: rgba(255,255,255,0.5); line-height: 1.5; max-width: 200px; margin: 0 auto; }
.numbers-source {
  text-align: center; margin-top: 40px; font-size: 13px; color: rgba(255,255,255,0.3);
  font-style: italic;
}

@media (max-width: 900px) {
  .numbers-grid { grid-template-columns: repeat(2, 1fr); }
  .number-item:nth-child(3n) { border-right: 1px solid rgba(255,255,255,0.08); }
  .number-item:nth-child(2n) { border-right: none; }
  .number-item:nth-last-child(-n+3) { border-bottom: 1px solid rgba(255,255,255,0.08); }
  .number-item:nth-last-child(-n+2) { border-bottom: none; }
}
@media (max-width: 640px) {
  .numbers-grid { grid-template-columns: 1fr 1fr; }
  .number-item { padding: 28px 16px; }
}
```

- [ ] **Step 2: Add plan HTML**

Insert after the guide section:

```html
<!-- ═══ 3-STEP PLAN ═══ -->
<section class="section section--navy" id="plan">
  <div class="container">
    <div class="plan-header reveal">
      <div class="badge badge-dark" style="margin: 0 auto 20px; display: inline-flex;">The Process</div>
      <h2>Getting Started Is Simple</h2>
      <p>Three steps. No complexity. No recruitment headaches. Just a conversation, then we handle the rest.</p>
    </div>

    <div class="plan-steps">
      <div class="plan-step reveal d1">
        <div class="plan-step-num">1</div>
        <h3>Get in Touch</h3>
        <p>Tell us about your PCN and your MSK demand. We'll walk you through how the service works and whether we're the right fit. No obligation.</p>
      </div>
      <div class="plan-step reveal d2">
        <div class="plan-step-num">2</div>
        <h3>We Handle Everything</h3>
        <p>We recruit and place a qualified FCP into your practice. Supervision, training, cover, and clinical governance are all managed by us. Your only job is to point MSK patients in the right direction.</p>
      </div>
      <div class="plan-step reveal d3">
        <div class="plan-step-num">3</div>
        <h3>Your GPs Get Their Time Back</h3>
        <p>MSK patients are seen faster by the right clinician. GP capacity opens up. You receive monthly outcome reports. And you didn't have to recruit a single person.</p>
      </div>
    </div>

    <div class="plan-cta reveal">
      <a href="#footer-cta" class="btn btn-primary">
        Get in Touch
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
      </a>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Add "What Sets Us Apart" HTML**

```html
<!-- ═══ WHAT SETS US APART ═══ -->
<section class="section" id="apart">
  <div class="container">
    <div class="apart-header reveal">
      <div class="badge" style="margin-bottom: 20px;">Why First Point Physio</div>
      <h2>What Sets Us Apart</h2>
      <p>We're not the biggest FCP provider. That's the point.</p>
    </div>

    <div class="apart-grid">
      <div class="apart-card reveal d1">
        <div class="apart-card-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
        </div>
        <h3>Personalised Service</h3>
        <p>As a small, agile provider, we offer a highly personalised service model aligned with the operational and clinical priorities of each PCN. We collaborate closely with our partners to ensure every facet of our service is responsive, adaptable, and customised to meet the unique needs of their member practices.</p>
      </div>

      <div class="apart-card reveal d2">
        <div class="apart-card-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>
        </div>
        <h3>Clinical Development</h3>
        <p>All clinicians are supported through structured professional development pathways and remain up to date with current best practice and regulatory standards.</p>
      </div>

      <div class="apart-card reveal d3">
        <div class="apart-card-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>
        </div>
        <h3>Performance Reporting</h3>
        <p>Monthly bespoke reports with clinic-level utilisation, outcomes, and patient feedback — enabling informed decisions and clear governance.</p>
      </div>

      <div class="apart-card reveal d4" style="grid-column: 2 / 3;">
        <div class="apart-card-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
        </div>
        <h3>Responsive Communication</h3>
        <p>Solution-focused, same-day resolution. No escalation tiers. The director answers his phone.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Add numbers HTML**

```html
<!-- ═══ THE NUMBERS ═══ -->
<section class="section section--navy" id="numbers">
  <div class="container">
    <div class="numbers-header reveal">
      <div class="badge badge-dark" style="margin: 0 auto 20px; display: inline-flex;">The Results</div>
      <h2>The Numbers Speak</h2>
      <p>Real data from our monthly PCN reports and the National FCP Evaluation.</p>
    </div>

    <div class="numbers-grid">
      <div class="number-item reveal d1">
        <div class="number-val">87<span>%</span></div>
        <div class="number-label">of patients managed within the service with no onward referral</div>
      </div>
      <div class="number-item reveal d2">
        <div class="number-val">98<span>%</span></div>
        <div class="number-label">appointment utilisation rate across all clinics</div>
      </div>
      <div class="number-item reveal d3">
        <div class="number-val">94<span>%</span></div>
        <div class="number-label">of patients would recommend the FCP service to others</div>
      </div>
      <div class="number-item reveal d1">
        <div class="number-val">80<span>%</span></div>
        <div class="number-label">didn't need to visit their GP for the same problem again</div>
      </div>
      <div class="number-item reveal d2">
        <div class="number-val">50<span>+</span></div>
        <div class="number-label">qualified clinicians delivering FCP services across the UK</div>
      </div>
      <div class="number-item reveal d3">
        <div class="number-val">120<span>+</span></div>
        <div class="number-label">GP surgeries with embedded First Point Physio clinicians</div>
      </div>
    </div>

    <p class="numbers-source reveal">From our monthly PCN performance reports and the National Evaluation of First Contact Practitioners</p>
  </div>
</section>
```

- [ ] **Step 5: Verify and commit**

Check: plan steps on navy background, differentiator cards in asymmetric grid, numbers as oversized typography with border dividers. Mobile: all stack.

```bash
git add demo2.html
git commit -m "Add plan, differentiators, and numbers sections"
```

---

### Task 5: Add Service overview, Case Study CTA, Footer, and final polish

**Files:**
- Modify: `demo2.html`

- [ ] **Step 1: Add CSS for service, case study, and footer**

```css
/* ═══ SERVICE OVERVIEW ═══ */
.service-grid { display: grid; grid-template-columns: 1.1fr 0.9fr; gap: 48px; align-items: start; }
.service-list h2 {
  font-size: clamp(28px, 4vw, 42px); font-weight: 800; letter-spacing: -0.025em;
  margin-bottom: 32px;
}
.service-list ul { display: flex; flex-direction: column; gap: 16px; }
.service-list li {
  display: flex; align-items: flex-start; gap: 14px;
  font-size: 16px; line-height: 1.65; color: var(--text-2);
}
.service-list li svg {
  flex-shrink: 0; width: 22px; height: 22px; stroke: var(--blue-bright);
  stroke-width: 2.5; margin-top: 2px;
}

.service-callout {
  padding: 40px 32px; border-radius: var(--r-xl);
  background: linear-gradient(145deg, var(--teal-bg-soft), rgba(176,212,223,0.3));
  border: 1px solid rgba(19,92,160,0.1);
}
.service-callout h3 { font-size: 20px; font-weight: 700; margin-bottom: 16px; color: var(--navy); }
.service-callout p { font-size: 15px; line-height: 1.75; color: var(--text-2); }
.service-callout .callout-highlight {
  margin-top: 20px; padding: 16px 20px; background: var(--white); border-radius: var(--r-lg);
  font-family: var(--heading); font-size: 15px; font-weight: 700; color: var(--blue);
  display: flex; align-items: center; gap: 10px;
}
.service-callout .callout-highlight svg { width: 20px; height: 20px; stroke: var(--blue-bright); flex-shrink: 0; }

@media (max-width: 900px) {
  .service-grid { grid-template-columns: 1fr; }
}

/* ═══ CASE STUDY CTA ═══ */
.case-study {
  background: linear-gradient(155deg, var(--navy), #0a2a54 60%, #051d40 100%);
  position: relative; overflow: hidden;
}
.case-study::before {
  content: ''; position: absolute; top: -150px; right: -100px; width: 400px; height: 400px;
  border-radius: 50%; background: radial-gradient(circle, rgba(86,174,255,0.08), transparent 65%);
  pointer-events: none;
}
.case-study-inner {
  max-width: 640px; margin: 0 auto; text-align: center; position: relative; z-index: 2;
}
.case-study h2 { color: var(--white); font-size: clamp(26px, 4vw, 36px); font-weight: 800; letter-spacing: -0.02em; margin-bottom: 16px; }
.case-study-sub { font-size: 17px; color: rgba(255,255,255,0.55); line-height: 1.75; margin-bottom: 32px; }
.case-study-form {
  display: flex; gap: 12px; max-width: 460px; margin: 0 auto;
}
.case-study-form input {
  flex: 1; padding: 16px 20px; border: 2px solid rgba(255,255,255,0.15);
  background: rgba(255,255,255,0.06); border-radius: var(--r-full);
  font-family: var(--body); font-size: 15px; color: var(--white);
  transition: border-color 0.3s;
}
.case-study-form input::placeholder { color: rgba(255,255,255,0.35); }
.case-study-form input:focus { outline: none; border-color: var(--sky); background: rgba(255,255,255,0.1); }
.case-study-form .btn { flex-shrink: 0; }

@media (max-width: 640px) {
  .case-study-form { flex-direction: column; }
  .case-study-form .btn { width: 100%; }
}

/* ═══ FOOTER ═══ */
.footer {
  background: var(--navy); padding: 80px 0 0; color: rgba(255,255,255,0.6);
}
.footer-cta-block {
  text-align: center; padding-bottom: 64px;
  border-bottom: 1px solid rgba(255,255,255,0.08);
}
.footer-cta-block h2 { color: var(--white); font-size: clamp(26px, 4vw, 36px); font-weight: 800; margin-bottom: 12px; }
.footer-cta-block p { font-size: 17px; color: rgba(255,255,255,0.45); margin-bottom: 32px; }
.footer-contacts {
  display: flex; justify-content: center; gap: 32px; flex-wrap: wrap; margin-bottom: 32px;
}
.footer-contact {
  display: inline-flex; align-items: center; gap: 10px;
  font-family: var(--heading); font-size: 16px; font-weight: 600; color: var(--white);
  transition: color 0.2s;
}
.footer-contact:hover { color: var(--sky); }
.footer-contact svg { width: 20px; height: 20px; stroke: var(--sky); flex-shrink: 0; }

.footer-bottom {
  display: flex; align-items: center; justify-content: space-between;
  padding: 28px 0; font-size: 13px;
}
.footer-bottom a { transition: color 0.2s; }
.footer-bottom a:hover { color: var(--sky); }

@media (max-width: 640px) {
  .footer-contacts { flex-direction: column; align-items: center; gap: 16px; }
  .footer-bottom { flex-direction: column; gap: 12px; text-align: center; }
}
```

- [ ] **Step 2: Add service overview HTML**

Insert after the numbers section:

```html
<!-- ═══ SERVICE OVERVIEW ═══ -->
<section class="section" id="service">
  <div class="container">
    <div class="service-grid">
      <div class="service-list reveal">
        <div class="badge" style="margin-bottom: 20px;">What's Included</div>
        <h2>Everything Included. One Price.</h2>
        <ul>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Qualified Band 7+ First Contact Practitioner placed in your practice</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Full recruitment and vetting — you don't lift a finger</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Clinical supervision and ongoing CPD for every clinician</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Holiday cover and sickness cover as standard</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Monthly outcome and activity reporting bespoke to your PCN</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>ARRS-funding aligned — one transparent price, fully refundable within the scheme</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Flexible engagement — stay because you want to, not because you're locked in</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Face-to-face, telephone, online, or enhanced access — whatever your practice needs</span></li>
        </ul>
      </div>
      <div class="service-callout reveal d2">
        <h3>Fully Funded Within ARRS</h3>
        <p>Our service is fully encompassed in our pricing and is completely refundable within the limits of the Additional Roles Reimbursement Scheme. No hidden costs, no surprise invoices — just one simple price that your ARRS allocation covers.</p>
        <div class="callout-highlight">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg>
          100% refundable within ARRS limits
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Add case study CTA HTML**

```html
<!-- ═══ CASE STUDY CTA ═══ -->
<section class="section case-study" id="case-study">
  <div class="container">
    <div class="case-study-inner reveal">
      <div class="badge badge-dark" style="margin: 0 auto 20px; display: inline-flex;">See the Evidence</div>
      <h2>See the Results for Yourself</h2>
      <p class="case-study-sub">Download our case study showing how a PCN freed up GP time and put ARRS funding to work with First Point Physio.</p>
      <form class="case-study-form" onsubmit="return false;">
        <input type="email" placeholder="Your work email address" required aria-label="Work email address">
        <button type="submit" class="btn btn-primary btn-sm">Download</button>
      </form>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Add footer HTML**

```html
<!-- ═══ FOOTER ═══ -->
<footer class="footer" id="footer-cta">
  <div class="container">
    <div class="footer-cta-block reveal">
      <h2>Ready to Free Up Your GP Appointments?</h2>
      <p>Let's have a conversation about how First Point Physio can work for your PCN.</p>
      <div class="footer-contacts">
        <a href="mailto:info@firstpointphysio.co.uk" class="footer-contact">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
          info@firstpointphysio.co.uk
        </a>
        <a href="tel:+447731526103" class="footer-contact">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
          Phillip Dale — 07731 526 103
        </a>
      </div>
      <a href="mailto:info@firstpointphysio.co.uk?subject=First%20Point%20Physio%20—%20Enquiry" class="btn btn-primary">
        Get in Touch
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
      </a>
    </div>

    <div class="footer-bottom">
      <span>&copy; 2026 First Point Physio Ltd. All rights reserved.</span>
      <span><a href="https://www.firstpointphysio.co.uk">firstpointphysio.co.uk</a></span>
    </div>
  </div>
</footer>
```

- [ ] **Step 5: Add print styles and responsive final polish**

Add before `</style>`:

```css
/* ═══ PRINT ═══ */
@media print {
  .nav, .marquee, .grain { display: none !important; }
  .section--navy { background: #f5f5f5; color: #1a1a1a; }
  .section--navy h2, .section--navy h3 { color: #1a1a1a; }
  .section--navy p, .section--navy .number-label { color: #555; }
  .number-val { color: #135ca0; }
  .number-val span { color: #135ca0; }
  .plan-step, .apart-card, .benefit-card { border: 1px solid #ddd; break-inside: avoid; }
  .case-study { background: #f5f5f5; }
  .case-study h2 { color: #1a1a1a; }
  .footer { background: #f5f5f5; }
  .footer h2 { color: #1a1a1a; }
  body { background: white; }
}
```

- [ ] **Step 6: Verify complete page and commit**

Full review:
- Nav renders on navy, burger works on mobile
- Hero split-screen: text left, image right
- Marquee scrolls infinitely
- Stakes left-aligned, empathetic tone
- Benefits in asymmetric grid with accent bar on hover
- Guide: empathy text + stat grid with oversized numbers
- Plan: 3 steps on navy background
- Differentiators: asymmetric grid
- Numbers: oversized typography, border dividers
- Service: checklist + ARRS callout card
- Case study: email capture form
- Footer: contacts + CTA
- Mobile: everything stacks, buttons full-width, tap-to-call
- Print: readable, dark backgrounds convert to light

```bash
git add demo2.html
git commit -m "Add service overview, case study CTA, footer, and print styles"
```
