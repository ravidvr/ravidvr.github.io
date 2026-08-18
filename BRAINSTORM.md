# Brainstorm: ravidvr.github.io — Recruiter + Project Dual-Audience Update

## What's There Now (live site, 2 projects)

- Header: name, 2-sentence tagline (12 years in data, Delivery Hero/Zalando), 3 links
- 2 project cards: getlos cinema map + German Worker Co-ops
- Footer with hidden Impressum
- No professional timeline, no skills, no resume link, no "open to work" signal
- Local working copy has 4 projects (adds Berlin Property Market + Mietspiegel Digitization)

## Gap Analysis

| What recruiters look for | Present? |
|---|---|
| Role/title immediately visible | ❌ No title anywhere |
| Employer timeline | ❌ Vague "over twelve years" |
| Hard skills (tools) | ❌ Nowhere on page |
| Location confirmation | ⚠️ Only in tagline body text |
| Open to work signal | ❌ |
| Resume download | ❌ |
| LinkedIn link | ✅ Primary CTA |
| Proof of competence (projects) | ✅ Strong, real, deployed |

**Core problem:** A recruiter landing here sees a hobbyist project page, not a Senior Data Analyst's portfolio. The projects are excellent proof of skill but the framing is wrong.

---

## Recommended Changes (ranked by impact/effort)

### 1. 🔴 HIGH — Rewrite page title + meta description (effort: trivial)

**Current:**
```
<title>Ravi Dronamraju — Berlin open-data projects</title>
<meta name="description" content="Ravi Dronamraju is a data analyst in Berlin. He builds free open-data maps: cinema showtimes and worker co-ops.">
```

**Proposed:**
```
<title>Ravi Dronamraju — Senior Data Analyst, Berlin</title>
<meta name="description" content="Senior Data Analyst in Berlin with 12 years experience at Delivery Hero, Zalando, and OLX. SQL, Python, A/B testing, experimentation. Open to work.">
```

This is the single highest-leverage change. Page titles are what recruiters see in search results, link previews, and browser tabs. "Berlin open-data projects" signals hobbyist. "Senior Data Analyst, Berlin" signals professional.

Also update `og:title` and `og:description` to match.

---

### 2. 🔴 HIGH — Add a role line + "open to work" below name (effort: 2 lines of HTML)

Right now `h1` says just "Ravi Dronamraju". A recruiter scans the page in 3 seconds and doesn't know what he does.

**Add immediately below h1:**
```html
<p class="role">Senior Data Analyst · Berlin · Open to opportunities</p>
```

**New CSS:**
```css
.role { font-size: 15px; color: var(--accent2); font-weight: 600; margin-top: 6px; }
```

This answers the 3 questions every recruiter has in the first scan: Who? What role? Where? Available?

The "Open to opportunities" phrase is professional and neutral — it works for both full-time and contract inquiries without sounding desperate.

---

### 3. 🟡 MEDIUM — Add a compact experience timeline (effort: ~30 lines of HTML/CSS)

Replace or augment the current prose tagline with a scannable timeline. The current tagline is warm and human but a recruiter needs to know *where* and *when* in 2 seconds.

**Proposed: replace the paragraph tagline with:**

```html
<div class="experience">
  <div class="exp-item">
    <span class="exp-year">2022–2026</span>
    <span class="exp-role">Senior Data Analyst</span>
    <span class="exp-company">@ Delivery Hero</span>
  </div>
  <div class="exp-item">
    <span class="exp-year">2022</span>
    <span class="exp-role">Senior Data Analyst</span>
    <span class="exp-company">@ OLX</span>
  </div>
  <div class="exp-item">
    <span class="exp-year">2019–2022</span>
    <span class="exp-role">Data Analyst</span>
    <span class="exp-company">@ Zalando</span>
  </div>
</div>
<p class="tagline">In my free time I build free, open-data maps that show what's happening in Berlin.</p>
```

**Opinion:** Cut the "I love working with data" opener — the projects and timeline prove that. Keep only the last sentence as a transition into the projects section. The timeline *is* the professional introduction.

Keep the CSS minimal — no icons, no fancy timeline lines. Just clean text rows.

---

### 4. 🟡 MEDIUM — Add a compact skills row (effort: ~10 lines HTML/CSS)

Yes, skills bar — but not a visual progress-bar monstrosity. Just a single text row of comma-separated keywords.

**Proposed (after experience, before "In my free time..."):**
```html
<div class="skills">SQL · BigQuery · Python · A/B Testing · Tableau · Looker · Experimentation · ETL</div>
```

```css
.skills { font-size: 13px; color: var(--text-dim); margin-top: 14px; letter-spacing: 0.3px; }
```

This is for ATS keyword matching via the meta description *and* for human recruiters who Ctrl+F for "BigQuery" or "Python". No icons, no rating bars, no complexity.

---

### 5. 🟢 LOW — Resume download link (effort: 1 link)

Add a resume link in the header button group. Option: host the PDF in the same repo or link to a Google Drive/Dropbox.

```html
<a href="resume.pdf">📄 Resume</a>
```

Don't make it the primary CTA (LinkedIn still is) — just a quiet option. If privacy is a concern (phone number on resume), skip it. The LinkedIn profile serves the same function. **Opinion: skip it unless there's content on the resume not on LinkedIn.** The site's minimalism is a feature.

---

### 6. 🟢 LOW — Design credibility tweaks (effort: ~15 lines CSS)

Two small changes that signal "professional" not "side project":

**a) Add a subtle header divider or background tint.**
The current all-white-on-light-gray looks clean but also looks like every un-styled personal page. A 2px accent border on the header bottom adds structure:
```css
header { border-bottom: 2px solid var(--accent2); padding-bottom: 36px; }
```

**b) Make the accent colors feel more "data professional."**
Current red (`#e63946`) on project buttons is fine for cinema flair but an all-blue palette (or blue + warm gray) reads more "analyst." Consider replacing `--accent: #e63946` with `#2a9d8f` (teal) or just go all-blue:
```css
--accent: #023e8a; --accent2: #0077b6;
```

**Opinion: keep the red.** It's distinctive, warm, and the projects (cinema, co-ops) are human-interest topics where red works. Blue-only feels sterile for this content.

---

### 7. 🟢 LOW — Contact section (effort: ~5 lines HTML)

Add a one-liner at the bottom of main (before footer): "Interested in working together? Reach out on LinkedIn or via email." This closes the loop for recruiters who scrolled through projects and are ready to act. Currently they have to scroll back up to find the email link.

---

## What Should NOT Change

| Keep | Why |
|---|---|
| Single-file HTML, no dependencies | This is the site's superpower. No build step, no framework, instant load. |
| Obfuscated email | Privacy matters. Keep the runtime JavaScript decoding. |
| Card-based project layout | It scales well (local copy already at 4 cards, could go to 6). |
| Hidden Impressum pattern | Required for German law, clever implementation. |
| System font stack | No web font requests, renders instantly on every device. |
| No analytics/tracking | Respects visitors. Don't add Google Analytics. |
| The "free maps" framing in tagline | Shows values — open data, public good. Differentiates from generic portfolio. |
| Warm, human tone of tagline (keep last sentence) | "I build free maps that show what is happening in Berlin" is memorable and specific. |

---

## Proposed New Header Section (complete, for reference)

```html
<header>
  <div class="wrap">
    <h1>Ravi Dronamraju</h1>
    <p class="role">Senior Data Analyst · Berlin · Open to opportunities</p>

    <div class="experience">
      <div class="exp-item">
        <span class="exp-year">2022–2026</span>
        <span class="exp-company">Delivery Hero</span>
        <span class="exp-context">— Supply Chain & Quick Commerce</span>
      </div>
      <div class="exp-item">
        <span class="exp-year">2022</span>
        <span class="exp-company">OLX</span>
        <span class="exp-context">— Experimentation Frameworks</span>
      </div>
      <div class="exp-item">
        <span class="exp-year">2019–2022</span>
        <span class="exp-company">Zalando</span>
        <span class="exp-context">— Product Analytics & A/B Testing</span>
      </div>
    </div>

    <div class="skills">SQL · BigQuery · Python · A/B Testing · Tableau · Looker · Experimentation · ETL</div>

    <p class="tagline">In my free time I build free, open-data maps that show what's happening in Berlin.</p>

    <div class="links">
      <a class="primary" href="https://www.linkedin.com/in/ravidvr/">in&nbsp; LinkedIn</a>
      <a href="https://github.com/ravidvr">GitHub</a>
      <a id="mailBtn" href="#">Email</a>
    </div>
  </div>
</header>
```

---

## Summary of Changes

| # | What | Impact | Effort | Lines |
|---|---|---|---|---|
| 1 | Rewrite title + meta/OG tags | Recruiters find the site | 4 lines | ~6 |
| 2 | Role line + open-to-work | Answers "who/what/where" instantly | 3 lines HTML + 1 CSS | ~4 |
| 3 | Experience timeline | Proves seniority at recognizable brands | 30 lines HTML + CSS | ~35 |
| 4 | Skills keyword row | ATS/discoverability, recruiter Ctrl+F | 2 lines HTML + 1 CSS | ~3 |
| 5 | Resume link (debatable) | Optional PDF download | 1 line | 1 |
| 6 | Contact CTA at bottom | Closes the loop for recruiters | 5 lines | 5 |
| 7 | ~Design tweaks | Professional polish | Optional | ~15 |

**Total:** ~70 lines added. File goes from ~150 to ~220 lines. Still single-file, still instant load, still no dependencies.

## Recommendation

Do **#1, #2, #3, and #4** — these 4 changes together transform the page from "hobbyist project list" to "senior professional's portfolio" in under 60 lines. Skip #5 (resume) unless there's content not on LinkedIn. Add #6 (contact CTA) if you want a soft close.

The minimalism *is* the strength. Don't add sections, don't add visual complexity. Just make the information architecture serve both audiences from the first scroll.
