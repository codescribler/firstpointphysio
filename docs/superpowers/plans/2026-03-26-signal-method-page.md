# Signal Method Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Signal Method page (`signal-method.html`) that explains the StoryBrand messaging strategy behind the First Point Physio website copy, using the existing project design system.

**Architecture:** Single self-contained HTML file using the same layout pattern as `proposal.html` (sticky header + TOC sidebar + content area). All CSS inline in a `<style>` block. Content sourced from the BrandScript (`projectcontext/First-Point-Physio-StoryBrand-Website-Brief.md`) and the Signal Method instructions (`projectcontext/signal-method-page-instructions.md`). New CSS components added for feature cards, before/after comparison cards, framework steps, and visitor journey table.

**Tech Stack:** HTML5, CSS3, vanilla JavaScript (scroll tracking, reveal animations)

**Reference files:**
- Layout/CSS base: `proposal.html` (lines 1–368 for CSS, 370–928 for HTML structure)
- Additional component patterns: `sample.html` (opp-cards for before/after, scope-cards for feature cards, strat-steps for numbered steps)
- Content source: `projectcontext/First-Point-Physio-StoryBrand-Website-Brief.md`
- Structure guide: `projectcontext/signal-method-page-instructions.md`
- Design spec: `docs/superpowers/specs/2026-03-26-signal-method-page-design.md`

---

### Task 1: Create signal-method.html with boilerplate, CSS, and Cover Page

**Files:**
- Create: `signal-method.html`

- [ ] **Step 1: Create the file with full `<head>`, CSS variables, and base styles**

Create `signal-method.html` with:
- Clarity analytics script (same as proposal.html)
- Meta tags: charset, viewport, `noindex nofollow`, title "The Messaging Strategy Behind Your New Website — First Point Physio"
- Google Fonts: Figtree + Noto Sans (same link as proposal.html)
- CSS `:root` variables — copy exactly from proposal.html lines 20–55
- Base reset, body styles, grain overlay — copy from proposal.html lines 57–74
- Sticky header CSS (`.prop-header` etc.) — copy from proposal.html lines 77–105
- TOC sidebar CSS (`.toc` etc.) — copy from proposal.html lines 113–133
- Layout grid CSS (`.prop-layout`, `.prop-content`) — copy from proposal.html lines 108–136
- Title block CSS (`.prop-title-block`) — copy from proposal.html lines 139–152
- Section heading CSS (`.prop-section`, `.section-num`, h2, h3, h4) — copy from proposal.html lines 155–176
- Body text and list CSS — copy from proposal.html lines 178–196
- Callout CSS — copy from proposal.html lines 199–206
- Table CSS (`.table-wrap`, `.prop-table`) — copy from proposal.html lines 220–262
- Horizontal rule CSS (`.prop-hr`) — copy from proposal.html lines 264–268
- CTA footer CSS (`.prop-cta`, `.btn-cta`) — copy from proposal.html lines 270–302
- Site footer CSS (`.prop-footer`) — copy from proposal.html lines 304–308

Add these NEW CSS components (not in proposal.html):

```css
/* ═══ FEATURE CARDS (2-col grid) ═══ */
.feature-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 32px 0; }
.feature-card {
  padding: 28px 24px; background: var(--white); border: 1px solid var(--border-light);
  border-radius: var(--r-xl); transition: all 0.35s ease; position: relative; overflow: hidden;
}
.feature-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  background: linear-gradient(90deg, var(--primary), var(--teal-400));
  transform: scaleX(0); transition: transform 0.4s ease; transform-origin: left;
}
.feature-card:hover { transform: translateY(-3px); box-shadow: 0 12px 32px rgba(0,0,0,0.06); border-color: transparent; }
.feature-card:hover::before { transform: scaleX(1); }
.feature-card-icon {
  width: 48px; height: 48px; border-radius: var(--r-md); background: rgba(11,114,133,0.08);
  display: flex; align-items: center; justify-content: center; margin-bottom: 16px;
}
.feature-card-icon svg { width: 24px; height: 24px; stroke: var(--primary); stroke-width: 1.8; }
.feature-card h4 { font-family: var(--heading); font-size: 17px; font-weight: 700; color: var(--text); margin-bottom: 8px; }
.feature-card p { font-size: 14.5px; line-height: 1.65; color: var(--text-2); margin: 0; }

/* ═══ FRAMEWORK STEPS (SB7) ═══ */
.framework-steps { margin: 32px 0; display: flex; flex-direction: column; gap: 20px; }
.framework-step {
  display: flex; gap: 20px; padding: 24px; background: var(--white);
  border: 1px solid var(--border-light); border-radius: var(--r-lg);
  transition: all 0.3s ease;
}
.framework-step:hover { border-color: var(--primary); box-shadow: 0 4px 16px rgba(11,114,133,0.06); }
.framework-step-num {
  width: 44px; height: 44px; min-width: 44px; border-radius: 50%;
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  display: flex; align-items: center; justify-content: center;
  font-family: var(--heading); font-size: 16px; font-weight: 900; color: var(--white);
  box-shadow: 0 3px 12px rgba(11,114,133,0.25);
}
.framework-step-content { flex: 1; }
.framework-step-label {
  font-family: var(--heading); font-size: 11px; font-weight: 800;
  letter-spacing: 0.08em; text-transform: uppercase; color: var(--primary); margin-bottom: 4px;
}
.framework-step-title { font-family: var(--heading); font-size: 17px; font-weight: 700; color: var(--text); margin-bottom: 6px; }
.framework-step-desc { font-size: 14.5px; line-height: 1.65; color: var(--text-2); margin: 0; }

/* ═══ BEFORE/AFTER COMPARISON CARDS ═══ */
.compare-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 32px 0; }
.compare-card { padding: 28px 24px; border-radius: var(--r-xl); }
.compare-card-before {
  background: var(--bg-warm); border: 1px solid var(--border);
}
.compare-card-after {
  background: linear-gradient(145deg, var(--teal-50), rgba(204,251,241,0.5));
  border: 1px solid rgba(11,114,133,0.12);
}
.compare-card-label {
  display: inline-flex; align-items: center; gap: 8px;
  font-family: var(--heading); font-size: 12px; font-weight: 800;
  letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 20px;
}
.compare-card-before .compare-card-label { color: var(--text-muted); }
.compare-card-after .compare-card-label { color: var(--primary); }
.compare-card-label-icon {
  width: 24px; height: 24px; border-radius: 50%; display: flex;
  align-items: center; justify-content: center;
}
.compare-card-before .compare-card-label-icon { background: var(--border); }
.compare-card-before .compare-card-label-icon svg { stroke: var(--text-muted); }
.compare-card-after .compare-card-label-icon { background: rgba(11,114,133,0.1); }
.compare-card-after .compare-card-label-icon svg { stroke: var(--primary); }
.compare-card ul { display: flex; flex-direction: column; gap: 12px; list-style: none; padding: 0; margin: 0; }
.compare-card li {
  display: flex; align-items: flex-start; gap: 10px;
  font-size: 14.5px; line-height: 1.6; color: var(--text-2);
}
.compare-card li svg { flex-shrink: 0; width: 18px; height: 18px; margin-top: 3px; stroke-width: 2.5; }
.compare-card-before li svg { stroke: var(--text-light); }
.compare-card-after li svg { stroke: var(--emerald); }

/* ═══ SUCCESS HIGHLIGHT BOX ═══ */
.highlight-box {
  margin: 32px 0; padding: 24px 28px; border-radius: var(--r-lg);
  background: linear-gradient(145deg, var(--teal-50), rgba(204,251,241,0.4));
  border: 1px solid rgba(5,150,105,0.15);
}
.highlight-box p { font-size: 15.5px; line-height: 1.75; color: var(--primary-dark); margin: 0; }
.highlight-box ul { list-style: none; padding: 0; margin: 12px 0 0; }
.highlight-box li {
  display: flex; align-items: flex-start; gap: 10px; padding: 6px 0;
  font-size: 15px; line-height: 1.6; color: var(--primary-dark);
}
.highlight-box li svg { flex-shrink: 0; width: 18px; height: 18px; margin-top: 3px; stroke: var(--emerald); stroke-width: 2.5; }

/* ═══ BLOCKQUOTE ═══ */
.signal-quote {
  margin: 28px 0; padding: 24px 28px; border-left: 4px solid var(--primary);
  background: var(--teal-50); border-radius: 0 var(--r-md) var(--r-md) 0;
}
.signal-quote p { font-size: 17px; font-style: italic; color: var(--primary-dark); line-height: 1.75; margin: 0; }
.signal-quote cite {
  display: block; margin-top: 12px; font-size: 14px; font-style: normal;
  font-weight: 600; color: var(--text-muted);
}

/* ═══ PROCESS STEPS (Signal Method 4-step) ═══ */
.process-steps { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 28px 0; }
.process-step {
  padding: 24px 20px; background: var(--white); border: 1px solid var(--border-light);
  border-radius: var(--r-lg); text-align: center; transition: all 0.3s ease;
}
.process-step:hover { border-color: var(--primary); box-shadow: 0 4px 16px rgba(11,114,133,0.06); transform: translateY(-2px); }
.process-step-num {
  width: 36px; height: 36px; margin: 0 auto 12px; border-radius: 50%;
  background: var(--primary); display: flex; align-items: center; justify-content: center;
  font-family: var(--heading); font-size: 14px; font-weight: 900; color: var(--white);
}
.process-step h4 { font-family: var(--heading); font-size: 15px; font-weight: 700; color: var(--text); margin-bottom: 6px; }
.process-step p { font-size: 13.5px; line-height: 1.6; color: var(--text-muted); margin: 0; }

/* ═══ VISITOR JOURNEY TABLE ═══ */
.journey-table { width: 100%; border-collapse: collapse; font-size: 14.5px; }
.journey-table thead th {
  font-family: var(--heading); font-size: 12px; font-weight: 800;
  letter-spacing: 0.06em; text-transform: uppercase; color: var(--text-muted);
  padding: 14px 18px; text-align: left; background: var(--bg-cool);
  border-bottom: 2px solid var(--border);
}
.journey-table tbody td {
  padding: 14px 18px; border-bottom: 1px solid var(--border-light);
  vertical-align: top; line-height: 1.65; color: var(--text-2);
}
.journey-table tbody td:last-child { font-style: italic; color: var(--primary-dark); }
.journey-table tbody tr:last-child td { border-bottom: none; }
.journey-table tbody tr:hover { background: rgba(11,114,133,0.02); }
```

Add responsive overrides for the new components:

```css
@media (max-width: 640px) {
  .feature-cards { grid-template-columns: 1fr; }
  .compare-cards { grid-template-columns: 1fr; }
  .process-steps { grid-template-columns: 1fr; }
  .framework-step { flex-direction: column; gap: 12px; }
  .framework-step-num { width: 36px; height: 36px; min-width: 36px; font-size: 14px; }

  .journey-table thead { display: none; }
  .journey-table tbody tr {
    display: block; margin-bottom: 16px; padding: 16px;
    border: 1px solid var(--border); border-radius: var(--r-md); background: var(--white);
  }
  .journey-table tbody td {
    display: block; padding: 4px 0; border-bottom: none; font-size: 14px;
  }
  .journey-table tbody td:first-child {
    font-weight: 700; color: var(--text); font-size: 15px;
    padding-bottom: 8px; margin-bottom: 8px; border-bottom: 1px solid var(--border-light);
  }
  .journey-table tbody td:last-child { padding-top: 4px; }
}
```

Also copy the full responsive block from proposal.html (lines 311–367) and merge with the above.

- [ ] **Step 2: Add the HTML body structure — grain, header, layout grid, TOC sidebar, and cover/title block**

```html
<body>
  <!-- Grain -->
  <svg class="grain" aria-hidden="true"><filter id="g"><feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="4" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(#g)"/></svg>

  <!-- Sticky Header (same as proposal.html) -->
  <header class="prop-header" id="propHeader">
    <div class="prop-header-inner">
      <div class="prop-header-left">
        <img src="images/logo (1).jpg" alt="First Point Physio" class="prop-header-logo">
        <a href="index.html" class="prop-header-back">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M19 12H5"/><path d="m12 19-7-7 7-7"/></svg>
          <span>Back to overview</span>
        </a>
      </div>
      <div class="prop-header-right"></div>
    </div>
  </header>

  <!-- Layout -->
  <div class="prop-layout">
    <!-- TOC sidebar -->
    <aside class="toc" id="toc">
      <div class="toc-label">Contents</div>
      <ul class="toc-list">
        <li><a href="#s01" class="toc-link" data-section="s01">01 — The Problem</a></li>
        <li><a href="#s02" class="toc-link" data-section="s02">02 — The Signal Method</a></li>
        <li><a href="#s03" class="toc-link" data-section="s03">03 — The Seven-Part Story</a></li>
        <li><a href="#s04" class="toc-link" data-section="s04">04 — How This Shapes the Copy</a></li>
        <li><a href="#s05" class="toc-link" data-section="s05">05 — Why This Works</a></li>
        <li><a href="#s06" class="toc-link" data-section="s06">06 — Generic vs Signal Method</a></li>
        <li><a href="#s07" class="toc-link" data-section="s07">07 — In Summary</a></li>
        <li><a href="#s08" class="toc-link" data-section="s08">08 — What Happens Next</a></li>
      </ul>
    </aside>

    <!-- Content -->
    <main class="prop-content">
      <!-- Title block -->
      <div class="prop-title-block">
        <div style="display:inline-flex;align-items:center;gap:8px;padding:6px 16px;background:rgba(11,114,133,0.06);border:1px solid rgba(11,114,133,0.12);border-radius:100px;font-family:var(--heading);font-size:12px;font-weight:700;color:var(--primary);letter-spacing:0.06em;text-transform:uppercase;margin-bottom:20px;">Supplementary — Website Proposal</div>
        <h1>The Messaging Strategy Behind Your New Website</h1>
        <div class="prop-client">First Point Physio</div>
        <div class="prop-meta">
          <div><strong>Prepared for</strong> Phillip Dale — Director</div>
          <div><strong>Prepared by</strong> dreamfree — Daniel Whittaker</div>
        </div>
      </div>

      <!-- Sections go here (Tasks 2-5) -->

    </main>
  </div>
</body>
```

- [ ] **Step 3: Add the JavaScript and close the file**

Copy the TOC scroll tracking and header shadow JS from proposal.html (lines 903–925). The script block goes just before `</body>`.

- [ ] **Step 4: Verify the page loads in browser**

Open `signal-method.html` in a browser. Verify:
- Header renders with logo and back link
- TOC sidebar appears on desktop, hidden on mobile
- Title block shows badge, heading, client name, meta
- No console errors

- [ ] **Step 5: Commit**

```bash
git add signal-method.html
git commit -m "Add signal-method.html boilerplate with CSS and cover page"
```

---

### Task 2: Add Sections 1 and 2 (Problem + Signal Method Introduction)

**Files:**
- Modify: `signal-method.html`

- [ ] **Step 1: Add Section 1 — The Problem With Most Business Websites**

Insert after the title block closing `</div>`, before the sections comment:

```html
<!-- ═══ 01 ═══ -->
<section class="prop-section" id="s01">
  <span class="section-num">01</span>
  <h2>The Problem With Most Business Websites</h2>

  <p>Most businesses struggle with their website copy. They know what they do — they're experts at it — but when it comes to writing it down in a way that resonates with potential customers, they're stuck. The result? Websites that talk <em>about</em> the business instead of talking <em>to</em> the customer.</p>

  <p>This isn't their fault. Nobody teaches business owners how to write website copy. So they default to what they've seen — "Welcome to [business name]", a wall of text about their history and qualifications, and a contact page buried three clicks deep. It looks professional. It says nothing.</p>

  <p>The consequence is simple: visitors leave. Not because the business isn't good at what it does, but because the website didn't give them a reason to stay. It didn't name their problem, didn't show them a clear path forward, and didn't make them feel understood. Confused people don't convert. They click away.</p>

  <p>This is why we don't just design your website — we write the copy too. And we do it using a proven framework.</p>
</section>

<hr class="prop-hr">
```

- [ ] **Step 2: Add Section 2 — What Is The Signal Method?**

```html
<!-- ═══ 02 ═══ -->
<section class="prop-section" id="s02">
  <span class="section-num">02</span>
  <h2>What Is The Signal Method?</h2>

  <p>The Signal Method is Dreamfree's approach to writing website copy that converts. It's built on the StoryBrand framework — a messaging methodology created by Donald Miller, used by thousands of businesses worldwide. The core insight is deceptively simple: <strong>if you confuse, you lose.</strong></p>

  <p>The principle is storytelling structure applied to marketing. Every great story has a hero with a problem who meets a guide, receives a plan, and is called to action — avoiding failure and ending in success. The same structure works on a website. The difference? <strong>Your customer is the hero. Your business is the guide.</strong> Most websites get this backwards — they make the business the hero of the story. That's why they don't convert.</p>

  <div class="signal-quote">
    <p>"People don't buy the best products. They buy the products they can understand the fastest."</p>
    <cite>— Donald Miller, Building a StoryBrand</cite>
  </div>

  <p>But The Signal Method isn't just "using StoryBrand." It's a complete process that turns your expertise into clear, compelling copy:</p>

  <div class="process-steps">
    <div class="process-step">
      <div class="process-step-num">1</div>
      <h4>Interview</h4>
      <p>We sit down with you and ask the right questions about your business, your customers, and what makes you different.</p>
    </div>
    <div class="process-step">
      <div class="process-step-num">2</div>
      <h4>Transcribe &amp; Research</h4>
      <p>We transcribe the interview and combine it with market research, competitor analysis, and customer insight.</p>
    </div>
    <div class="process-step">
      <div class="process-step-num">3</div>
      <h4>BrandScript</h4>
      <p>We distil everything into a clear messaging framework that defines exactly what your website needs to say and why.</p>
    </div>
    <div class="process-step">
      <div class="process-step-num">4</div>
      <h4>Copy &amp; Build</h4>
      <p>We write every word of your website copy based on the BrandScript, then design and build the site around that message.</p>
    </div>
  </div>

  <p>You don't need to write a single word. We handle it — because most businesses shouldn't be writing their own website copy. Not because they can't write, but because they're too close to their own business to see it the way a customer does.</p>
</section>

<hr class="prop-hr">
```

- [ ] **Step 3: Verify sections render correctly**

Open in browser. Check:
- Section numbering and headings render
- Blockquote styling looks correct
- 4-step process cards display in 2x2 grid
- Mobile: process cards stack to single column

- [ ] **Step 4: Commit**

```bash
git add signal-method.html
git commit -m "Add sections 1-2: problem statement and Signal Method introduction"
```

---

### Task 3: Add Section 3 (The Seven-Part Story)

**Files:**
- Modify: `signal-method.html`

- [ ] **Step 1: Add Section 3 — The Seven-Part Story**

Insert after the Section 2 `<hr class="prop-hr">`:

```html
<!-- ═══ 03 ═══ -->
<section class="prop-section" id="s03">
  <span class="section-num">03</span>
  <h2>The Seven-Part Story</h2>

  <p>Every effective website follows the same narrative structure. Here's how we applied each element of the StoryBrand framework to the First Point Physio website — and the specific copy decisions behind each one.</p>

  <div class="framework-steps">
    <div class="framework-step">
      <div class="framework-step-num">1</div>
      <div class="framework-step-content">
        <div class="framework-step-label">A Character</div>
        <div class="framework-step-title">PCN Practice Managers and Clinical Directors who need a reliable FCP service</div>
        <p class="framework-step-desc">The hero of this website isn't First Point Physio — it's the practice manager responsible for commissioning FCP services within their Primary Care Network. Every headline, every section, every word is written for them.</p>
      </div>
    </div>

    <div class="framework-step">
      <div class="framework-step-num">2</div>
      <div class="framework-step-content">
        <div class="framework-step-label">Has a Problem</div>
        <div class="framework-step-title">"Your GPs are spending a third of their day on MSK cases they shouldn't need to see"</div>
        <p class="framework-step-desc">The problem isn't just practical (GP overload, recruitment difficulty) — it's emotional. Practice managers feel stretched, anxious, and frustrated. The copy names this directly in the "Sound Familiar?" section, so visitors feel understood before they're asked to do anything.</p>
      </div>
    </div>

    <div class="framework-step">
      <div class="framework-step-num">3</div>
      <div class="framework-step-content">
        <div class="framework-step-label">Meets a Guide</div>
        <div class="framework-step-title">First Point Physio — experienced, empathetic, and equipped</div>
        <p class="framework-step-desc">The website positions First Point Physio as the guide through two signals: <strong>empathy</strong> ("We Know the Pressure You're Under") and <strong>authority</strong> (Band 7+ FCPs, three regions, £30 vs £90 cost comparison, testimonials). Empathy without authority is weakness. Authority without empathy is arrogance. The site balances both.</p>
      </div>
    </div>

    <div class="framework-step">
      <div class="framework-step-num">4</div>
      <div class="framework-step-content">
        <div class="framework-step-label">Who Gives Them a Plan</div>
        <div class="framework-step-title">Book a Discovery Call → We Handle Everything → Your GPs Focus on What Matters</div>
        <p class="framework-step-desc">When people see a clear path, they take it. The 3-step plan reduces the perceived complexity of outsourcing an FCP from "daunting project" to "simple conversation." Each step is named to reassure: you talk, we work, you benefit.</p>
      </div>
    </div>

    <div class="framework-step">
      <div class="framework-step-num">5</div>
      <div class="framework-step-content">
        <div class="framework-step-label">And Calls Them to Action</div>
        <div class="framework-step-title">"Book a Discovery Call" — visible, repeated, consistent</div>
        <p class="framework-step-desc">The direct CTA appears in the navigation bar, the hero section, after the 3-step plan, in the service section, and in the footer. A transitional CTA — "Download Our Free PCN Guide" — catches visitors who aren't ready to talk yet but are willing to exchange their email.</p>
      </div>
    </div>

    <div class="framework-step">
      <div class="framework-step-num">6</div>
      <div class="framework-step-content">
        <div class="framework-step-label">That Helps Them Avoid Failure</div>
        <div class="framework-step-title">Wasted ARRS funding, GP burnout, months-long recruitment gaps</div>
        <p class="framework-step-desc">The "Sound Familiar?" section doesn't just name the current problem — it hints at what happens if nothing changes. ARRS funding goes unspent. GPs remain overloaded. Recruitment attempts drag on. The copy creates just enough tension to motivate action without resorting to fear-mongering.</p>
      </div>
    </div>

    <div class="framework-step">
      <div class="framework-step-num">7</div>
      <div class="framework-step-content">
        <div class="framework-step-label">And Ends in Success</div>
        <div class="framework-step-title">"Your GPs do what they trained for. Your patients get faster, better MSK care. Your ARRS funding works."</div>
        <p class="framework-step-desc">The "What Changes When You Work With Us" section paints the picture of life after: GP time reclaimed, ARRS budget utilised, zero operational burden, better patient outcomes. The visitor can see themselves in the success before they've even picked up the phone.</p>
      </div>
    </div>
  </div>
</section>

<hr class="prop-hr">
```

- [ ] **Step 2: Verify section renders**

Check:
- Seven framework steps display with numbered circles
- Labels appear in uppercase teal
- Titles are bold, descriptions are muted
- Mobile: steps stack vertically, number + content in column layout

- [ ] **Step 3: Commit**

```bash
git add signal-method.html
git commit -m "Add section 3: seven-part StoryBrand story framework"
```

---

### Task 4: Add Sections 4 and 5 (Copy Mapping + Why This Works)

**Files:**
- Modify: `signal-method.html`

- [ ] **Step 1: Add Section 4 — How This Shapes the Website Copy**

Insert after Section 3's `<hr class="prop-hr">`:

```html
<!-- ═══ 04 ═══ -->
<section class="prop-section" id="s04">
  <span class="section-num">04</span>
  <h2>How This Shapes the Website Copy</h2>

  <p>Every decision on the website — from headline wording to button placement — maps back to a Signal Method principle. Here's exactly what we did and why.</p>

  <div class="table-wrap">
    <table class="prop-table">
      <thead>
        <tr>
          <th>Signal Method Principle</th>
          <th>What We Did on the Site</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><strong>Customer is the hero</strong></td>
          <td data-label="What We Did">The headline reads "Free Up Your GPs. We Handle MSK." — it's about what <em>they</em> get, not what we do. The word "your" appears before "we" in every key section.</td>
        </tr>
        <tr>
          <td><strong>Name the problem</strong></td>
          <td data-label="What We Did">The "Sound Familiar?" section opens with: "Your GPs are spending a third of their day on musculoskeletal cases they shouldn't need to see." It names their exact daily reality.</td>
        </tr>
        <tr>
          <td><strong>Show empathy + authority</strong></td>
          <td data-label="What We Did">"We Know the Pressure You're Under" (empathy) paired with a stats bar — Band 7+ FCPs, 3 regions, £30 vs £90 (authority). The tone says "we get it" while the numbers say "we can do it."</td>
        </tr>
        <tr>
          <td><strong>Give them a plan</strong></td>
          <td data-label="What We Did">A 3-step process: "Book a Discovery Call → We Handle Everything → Your GPs Focus on What Matters." Reduces a complex outsourcing decision to three simple steps.</td>
        </tr>
        <tr>
          <td><strong>Repeat the CTA</strong></td>
          <td data-label="What We Did">"Book a Discovery Call" appears in the navigation bar, hero section, after the 3-step plan, in the service overview, and in the footer — five times on one page.</td>
        </tr>
        <tr>
          <td><strong>Remove friction</strong></td>
          <td data-label="What We Did">"One simple price — no hidden fees." "Flexible contract terms — we earn your trust, not lock you in." The service section includes a full checklist of what's included, eliminating ambiguity.</td>
        </tr>
        <tr>
          <td><strong>Paint success</strong></td>
          <td data-label="What We Did">"What Changes When You Work With Us" — four benefit cards showing life after: GP time reclaimed, ARRS funding working, zero burden, better outcomes. The visitor sees the result before they've acted.</td>
        </tr>
        <tr>
          <td><strong>Transparent pricing</strong></td>
          <td data-label="What We Did">"Each FCP appointment costs roughly £30 vs £90+ for an equivalent GP consultation." Stating cost early and clearly removes the biggest unspoken objection: "can we afford this?"</td>
        </tr>
      </tbody>
    </table>
  </div>
</section>

<hr class="prop-hr">
```

- [ ] **Step 2: Add Section 5 — Why This Helps Practice Managers Book a Discovery Call**

```html
<!-- ═══ 05 ═══ -->
<section class="prop-section" id="s05">
  <span class="section-num">05</span>
  <h2>Why This Helps Practice Managers Book a Discovery Call</h2>

  <p>The Signal Method isn't just a writing technique — it's applied psychology. Here are the four principles that make it work, followed by a walk-through of exactly what a visitor experiences on the homepage.</p>

  <h3>The Four Principles</h3>

  <div class="feature-cards">
    <div class="feature-card">
      <div class="feature-card-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
      </div>
      <h4>Clarity in 5 Seconds</h4>
      <p>The "Grunt Test" — could a caveman understand what you offer, how it helps, and what to do next within 5 seconds of landing? The hero section passes this test: managed FCPs, free up your GPs, book a discovery call.</p>
    </div>
    <div class="feature-card">
      <div class="feature-card-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/></svg>
      </div>
      <h4>Reduces Mental Effort</h4>
      <p>Confused visitors leave. Story structure gives the brain a familiar pattern to follow — problem, guide, plan, action — so visitors stay engaged without having to work out what to do next.</p>
    </div>
    <div class="feature-card">
      <div class="feature-card-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
      </div>
      <h4>Answers the Real Questions</h4>
      <p>Practice managers aren't just asking "what do you do?" They're asking "will this actually work for us?" and "will it create more problems?" The copy answers the emotional questions, not just the practical ones.</p>
    </div>
    <div class="feature-card">
      <div class="feature-card-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M12 8v8"/><path d="m8 12 4 4 4-4"/></svg>
      </div>
      <h4>Always a Clear Next Step</h4>
      <p>No dead ends. Every section on the homepage flows into the next, and every section ends with a path forward. The visitor is never left wondering "OK, now what?"</p>
    </div>
  </div>

  <h3>The Visitor Journey</h3>

  <p>Here's what happens inside a practice manager's head as they scroll through the homepage, section by section:</p>

  <div class="table-wrap">
    <table class="journey-table">
      <thead>
        <tr>
          <th>What They See</th>
          <th>What They Think</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><strong>Hero:</strong> "Free Up Your GPs. We Handle MSK."</td>
          <td>"That's exactly what I need. They get it."</td>
        </tr>
        <tr>
          <td><strong>Sound Familiar?</strong> — names their daily reality of GP overload and recruitment struggles</td>
          <td>"Yes. That's my life right now. Someone actually understands what we're dealing with."</td>
        </tr>
        <tr>
          <td><strong>What Changes:</strong> GP Time Reclaimed, ARRS Funding Working, Zero Burden, Better Outcomes</td>
          <td>"These are the things I actually care about. Not features — results."</td>
        </tr>
        <tr>
          <td><strong>"We Know the Pressure You're Under"</strong> — empathy statement with testimonial</td>
          <td>"They're not just selling to me — they've been in this world. They know how it feels."</td>
        </tr>
        <tr>
          <td><strong>3 Steps:</strong> Book → We Handle Everything → GPs Get Time Back</td>
          <td>"Simple. I don't have to figure anything out. Just book a call and they do the rest."</td>
        </tr>
        <tr>
          <td><strong>Stats bar:</strong> Band 7+, 3 regions, £30 vs £90+</td>
          <td>"The numbers stack up. This makes financial sense."</td>
        </tr>
        <tr>
          <td><strong>"Book a Discovery Call"</strong></td>
          <td>"Low risk. No commitment. I'll do it."</td>
        </tr>
      </tbody>
    </table>
  </div>

  <div class="highlight-box">
    <p>Practice managers don't book a discovery call because of features or qualifications. They book because the website made them feel <strong>confident</strong> — confident that their MSK problem will be handled competently, that the transition will be smooth, and that there won't be surprises.</p>
  </div>
</section>

<hr class="prop-hr">
```

- [ ] **Step 3: Verify both sections render**

Check:
- Section 4 table renders with two columns, hover state on rows
- Section 5 feature cards display in 2x2 grid
- Visitor journey table renders with italic right column
- Green highlight box renders at bottom
- Mobile: tables stack to card layout, feature cards go single column

- [ ] **Step 4: Commit**

```bash
git add signal-method.html
git commit -m "Add sections 4-5: copy mapping table and visitor psychology"
```

---

### Task 5: Add Sections 6, 7, 8 (Comparison + Summary + CTA) and Footer/JS

**Files:**
- Modify: `signal-method.html`

- [ ] **Step 1: Add Section 6 — Generic Copy vs Signal Method Copy**

Insert after Section 5's `<hr class="prop-hr">`:

```html
<!-- ═══ 06 ═══ -->
<section class="prop-section" id="s06">
  <span class="section-num">06</span>
  <h2>Generic Copy vs. Signal Method Copy</h2>

  <p>The easiest way to see the difference is side by side. Both descriptions could be for the same FCP provider — but only one is structured to help a practice manager <em>decide</em>.</p>

  <div class="compare-cards">
    <div class="compare-card compare-card-before">
      <div class="compare-card-label">
        <div class="compare-card-label-icon"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg></div>
        Typical FCP Provider Website
      </div>
      <ul>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg><span>Leads with "Welcome to [Company Name]"</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg><span>Opens with founding story and company history</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg><span>Lists services and qualifications without patient context</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg><span>One small contact link buried in navigation</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg><span>Visitor has to work out if it suits their PCN</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg><span>No clear path from interest to enquiry</span></li>
      </ul>
    </div>

    <div class="compare-card compare-card-after">
      <div class="compare-card-label">
        <div class="compare-card-label-icon"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg></div>
        The Signal Method
      </div>
      <ul>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg><span>Leads with what the practice manager wants</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg><span>Opens with their daily frustration and pain points</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg><span>Benefits framed around their operational reality</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg><span>CTA visible immediately and repeated throughout</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg><span>Site answers their objections proactively</span></li>
        <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg><span>Guided journey from problem to discovery call</span></li>
      </ul>
    </div>
  </div>

  <p>Both websites describe the same kind of service. The difference is that the Signal Method version is structured to help someone <em>decide</em>, not just <em>browse</em>.</p>
</section>

<hr class="prop-hr">
```

- [ ] **Step 2: Add Section 7 — In Summary**

```html
<!-- ═══ 07 ═══ -->
<section class="prop-section" id="s07">
  <span class="section-num">07</span>
  <h2>In Summary</h2>

  <p>The proposed website isn't just a visual upgrade — it's a fundamentally different approach to how First Point Physio communicates with potential PCN partners online.</p>

  <div class="highlight-box">
    <p>The Signal Method framework ensures that your website:</p>
    <ul>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Focuses on the customer's problem, not your company's history</span></li>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Acknowledges the emotional reality of managing a stretched practice team</span></li>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Removes doubt with empathy, authority, and transparent pricing</span></li>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Provides a simple, clear path from "I'm interested" to "I've booked a call"</span></li>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Repeats the call to action so no visitor is left wondering what to do next</span></li>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg><span>Paints a vivid picture of success so they can see the outcome before they act</span></li>
    </ul>
  </div>

  <p>Every word on the site was written with purpose — informed by a structured interview, real research, and a proven messaging framework. This isn't template copy. It's strategy.</p>

  <p><strong>The result is a website that doesn't just look good — it <em>works</em>.</strong></p>
</section>

<hr class="prop-hr">
```

- [ ] **Step 3: Add Section 8 — What Happens Next (CTA) and Footer**

```html
<!-- ═══ 08 ═══ -->
<section class="prop-section" id="s08">
  <span class="section-num">08</span>
  <h2>Ready to Talk About Your Website?</h2>

  <p>If what you've read here resonates — if you can see the difference between a website that talks about your business and one that talks to your customers — then the next step is a conversation.</p>

  <p>I'll listen, ask questions about your business, and explain how The Signal Method would apply to your specific situation. You'll come away with clarity on what's working, what isn't, and what a high-converting website could look like for you — whether we end up working together or not.</p>
</section>

<!-- ═══ CTA ═══ -->
<div class="prop-cta">
  <h2>Get in touch to discuss your website</h2>
  <p class="cta-sub">No commitment, no pressure. Just a conversation about how your website could work harder for your business.</p>
  <div class="prop-cta-contacts">
    <a href="mailto:daniel@dreamfree.co.uk" class="prop-cta-contact">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      daniel@dreamfree.co.uk
    </a>
    <a href="tel:+447786556885" class="prop-cta-contact">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
      07786 556 885
    </a>
  </div>
  <a href="mailto:daniel@dreamfree.co.uk?subject=First%20Point%20Physio%20—%20Signal%20Method%20Discussion" class="btn-cta">
    Get in touch
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
  </a>
</div>

    </main>
  </div>

  <!-- Footer -->
  <footer class="prop-footer">
    <img src="images/proposal/dreamfree.png" alt="dreamfree">
    <p>&copy; 2026 dreamfree. Prepared exclusively for First Point Physio.</p>
  </footer>
```

- [ ] **Step 4: Verify the complete page**

Open in browser. Full walkthrough:
- All 8 sections render with correct numbering
- TOC sidebar highlights active section on scroll
- Comparison cards display side by side (before grey, after green)
- Summary highlight box renders with checkmarks
- CTA section renders with email/phone links and orange button
- Footer shows dreamfree branding
- Mobile: all components stack correctly, tables become cards
- Print: page renders cleanly (optional check)

- [ ] **Step 5: Commit**

```bash
git add signal-method.html
git commit -m "Add sections 6-8: comparison, summary, and CTA with footer"
```

---

### Task 6: Final review and print styles

**Files:**
- Modify: `signal-method.html`

- [ ] **Step 1: Add print styles**

Add before the closing `</style>` tag:

```css
/* ═══ PRINT ═══ */
@media print {
  .prop-header, .toc, .grain { display: none !important; }
  .prop-layout { display: block; padding-top: 0; }
  .prop-content { max-width: 100%; }
  .prop-section { page-break-inside: avoid; margin-bottom: 40px; }
  .prop-hr { margin: 32px 0; }
  .framework-step, .feature-card, .compare-card { break-inside: avoid; }
  .table-wrap { border: 1px solid #ddd; }
  .prop-cta { background: #f5f5f5; color: #1a1a1a; }
  .prop-cta h2 { color: #1a1a1a; }
  .prop-cta .cta-sub { color: #555; }
  .prop-cta-contact { color: #1a1a1a; }
  .btn-cta { background: #333; }
  body { background: white; }
}
```

- [ ] **Step 2: Full visual review**

Review the complete page:
- Scroll through all sections for consistency
- Check no orphaned headings at page bottom
- Verify all links work (email, phone, back to overview)
- Check mobile at 375px width
- Check tablet at 768px width

- [ ] **Step 3: Commit**

```bash
git add signal-method.html
git commit -m "Add print styles and finalize signal method page"
```
