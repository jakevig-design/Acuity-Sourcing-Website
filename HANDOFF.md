# Acuity Sourcing — Project Handoff

This document is the working context for the **acuitysourcing.com** website. It captures architecture, decisions, file structure, and open work so that a new session can pick up the project without re-reading the full history.

Last updated: April 2026.

---

## 1. Project goal

Acuity Sourcing is a boutique IT sourcing consulting practice founded by Jake Vigneri. The website serves two purposes:

1. **Credibility validator.** Most business arrives through warm intros. The site exists so a CFO, VP, or referral partner who has heard Jake's name can confirm he's the real thing before taking a call.
2. **Acquisition surface.** A growing piece — readers who arrive via LinkedIn, podcasts, or content can decide whether to engage.

The site is **founder-forward** (Jake is the visible person, Acuity is the firm name) and uses **first-person voice throughout** ("I" not "we"). It launches alongside Pario, a software product Jake is building under the same parent (planwithpario.com), but the two sites do not visually integrate beyond a brand mention.

**Brand thesis (load-bearing):** *The work that decides a software deal happens before anyone calls a vendor, and it is the work that almost always gets skipped.*

**Positioning:** *Requirements-first shop.* This phrase is intentionally specific and runs through the hero, About, and Services pages. It distinguishes Acuity from generic procurement advisors.

---

## 2. Current architecture

**Static HTML site, deployed on Vercel from GitHub.**

- No framework. Each page is a self-contained `.html` file with embedded CSS and inline content.
- `vercel.json` enables clean URLs, so `/about` serves `about.html` without the extension showing.
- Auto-deploys on push to `main` of `jakevig-design/acuity-site`.
- Domain `acuitysourcing.com` is registered through Squarespace; DNS points at Vercel.
- LinkedIn company page exists separately and is partially populated; not the priority.

**Why static HTML, not Next.js:** Decision made deliberately to ship fast. The earlier site was also static HTML. Next.js conversion is parking-lot for a future session — the trigger to migrate is when the duplication of nav and CSS across pages becomes meaningfully painful (estimated: after 5+ essays, or when the nav structure changes).

**Tradeoffs of the current setup:**

- Nav block is duplicated across all five pages. Adding/removing a nav link means editing five files.
- CSS is embedded in each page. Updating a global style (color, font, spacing) means editing five files.
- No build step, no JavaScript framework, no component reuse.
- No CMS. Content edits happen by editing the HTML directly.

These tradeoffs are acceptable for the current pace of change but become limiting if the site's structure evolves significantly.

---

## 3. File structure

```
acuity-site/
├── index.html                              Home page (longest, most sections)
├── about.html                              About / origin story
├── work.html                               Selected Work / portfolio (7 case studies)
├── how-i-work.html                         Services / engagement models
├── writing/
│   └── software-expensive.html             Flagship essay ("Three Taxes")
├── vercel.json                             Clean URL config
├── HANDOFF.md                              This file
└── README.md                               Brief deployment notes
```

**Page → URL mapping:**

| Page | File | Live URL |
|------|------|----------|
| Home | `index.html` | `/` |
| About | `about.html` | `/about` |
| Selected Work | `work.html` | `/work` |
| How I Work (Services) | `how-i-work.html` | `/how-i-work` |
| Flagship Essay | `writing/software-expensive.html` | `/writing/software-expensive` |

---

## 4. Design system

### Typography
- **Display headlines (h1, h2):** Inter, 600 weight, tight letter-spacing (-0.025em)
- **Body text:** Inter, 400 weight, line-height 1.6–1.8
- **Utility (nav, labels, stats):** Inter, 500–700 weight, increased letter-spacing for small caps where used
- **Brand signature:** "Sourcing" word in nav-logo uses Fraunces italic — only retained italic Fraunces on the entire site
- **Inline italic emphasis** within prose (e.g., book titles, light emphasis in essay body) uses Fraunces italic

### Color palette (CSS variables, identical across all pages)

```css
:root {
  --bg: #f7f7f6;          /* Page background, neutral light gray */
  --bg-warm: #eeeeec;     /* Slightly darker section alternates */
  --ink: #131313;         /* Primary text, near-black */
  --ink-soft: #2a2a2a;    /* Body prose, softened */
  --ink-muted: #6a6a6a;   /* Labels, secondary text */
  --accent: #5e8b3f;      /* Moss green, sampled from logo */
  --accent-soft: #7fa85f; /* Hover states, dark-section treatment */
  --rule: #d8d8d5;        /* Dividers, borders */
  --paper: #ffffff;       /* Cards, inner sections */
  --max: 1120px;          /* Max content width on home page; varies on others */
}
```

**Accent green (#5e8b3f) is the only brand color.** It appears on: section labels, italicized emphasis words in headlines, link underlines, principle numbering (01/02/03), the principles' left border on `:last-child` quotes, and the drop cap on the essay page.

### Layout principles
- Max content width 1120px on the home page; narrower (680–820px) on inner pages for readability
- Generous vertical section padding (100px top/bottom on most sections)
- Section labels in small caps (`font-size: 12px; letter-spacing: 0.18em; text-transform: uppercase`) above each section headline
- The Pario section on the home page inverts to a dark background (`--ink` as bg) with green accent — the only inverted section on the site

---

## 5. Key decisions made (in order of consequence)

### Positioning
1. **Founder-forward, not firm-forward.** Site reads as "Jake's practice" not "Acuity Sourcing, the firm." First person throughout.
2. **Two-layer consulting positioning.** Site narrows to *pre-vendor / requirements / competitive bid* work as the lead. Broader practice (audit defense, license intelligence, post-M&A) is acknowledged on the Services page but not led with. Reasoning: the website's job is to attract the kind of work Jake wants more of, not to list everything he can do.
3. **Acuity and Pario kept visually separate.** Pario gets a dedicated section on the home page but the brands don't cross-link aggressively. They share founder and IP, not visual identity.
4. **Portfolio anonymized by industry + deal shape.** No client names. "Global Asset Management Firm" not "BlackRock." This is honest given the work was done as an employee, not as Acuity, and gives prospective clients confidence about discretion.

### Voice and content
5. **No em dashes anywhere.** Hard rule. Use commas, periods, or restructure.
6. **No "we" voice.** Always "I" — Acuity is a one-person practice. Don't pretend otherwise.
7. **Confident observer, not prosecutor.** When discussing buyer mistakes, frame as patterns (the system) rather than accusations (you, the reader).
8. **No absolutes.** "Most" and "often" rather than "always" or "every." Reasoning: a senior reader will catch any overclaim and lose trust.

### Visual
9. **Sage green as the only accent.** Sampled from the existing Acuity logo gradient.
10. **Inter (sans-serif) for body and display.** Earlier versions used Fraunces serif throughout; user feedback was that Fraunces italic read as "concert poster from 1969." Final design uses Inter for everything except the wordmark italic and inline prose italic.
11. **Principles section uses 01/02/03 utility numbering, not Roman numerals.** Earlier draft had italic Roman numerals (i. ii. iii.); user found them precious.

### Architecture
12. **Static HTML, not Next.js.** Decision made for ship-speed. Reconsider when the duplication tax becomes meaningful.
13. **Clean URLs via `vercel.json`.** All internal links omit `.html` extensions.

---

## 6. What's currently working

- ✅ Site is live at acuitysourcing.com
- ✅ All five pages deploy and route correctly via clean URLs
- ✅ Internal navigation links resolve across all pages
- ✅ External links to planwithpario.com and LinkedIn work
- ✅ Mailto link is functional
- ✅ Mobile rendering holds (responsive at 720px and 820px breakpoints)
- ✅ Vercel auto-deploys on push to main

---

## 7. What's broken or stale

**Critical (the deployed version is older than the latest local edits):**

The current live site reflects an earlier version of the design. The following were updated in subsequent local edits but **the updates have not been pushed to GitHub yet**:

1. **"Three claims. The work is built on them"** sub-headline still appears on the principles section. Should be removed entirely; section label "Principles" alone is sufficient.
2. **Roman numeral principle markers (i. ii. iii.)** still display. Should be replaced with utility-style 01 / 02 / 03 in Inter, accent green color.
3. **Italic emphasis on section headlines** still uses Fraunces italic. Should be plain text in accent green color (no italic, no serif).
4. **Body font is still Fraunces.** Should be Inter throughout the site.
5. **Acuity and Pario cards on the home page do not have aligned dividers.** The "How I work →" and "Try Pario →" CTAs sit at different vertical positions because the card content lengths differ. Fix: flexbox with `min-height` on h3 and card-for sections so dividers align.

**Fix required:** Re-deploy with the latest local versions. The HTML in this document (Section 9) reflects the *intended* state.

**Non-critical, parked:**

- About page may be too long; user wants to revisit after seeing live. Macmillan and Fed paragraphs are most trimmable.
- Principle #2 ("Information is currency") wording was flagged for one more pass; never finalized.
- About page has placeholder photo ("JV" in a circle). Real photo of Jake to be added.
- No Pario screenshot on home page Pario section (intentional placeholder — add when product UI is ready).
- LinkedIn company page exists but is partially populated. Sitting at "good enough."

---

## 8. Open work

### Site polish (immediate)
- Re-deploy latest local version to fix items 1–5 above
- Add real photo to About page
- Verify mobile rendering on actual phone

### Content pipeline (next 4–6 weeks)
- **Essay #2:** *It's Never Too Early to Call.* Already drafted as a LinkedIn post; needs to be polished into site-voice essay format and added to `/writing/`. Source post is in user's LinkedIn archive. Working title candidates: *"The Software Deal You're Losing Without Knowing It"* or original title.
- **Essay #3:** *The Procurement Cheat Code* / strategic coaching piece. Reframe for a non-procurement audience. Working title: *"Why I Coach Stakeholders Instead of Negotiating for Them."*
- **Essay #4 (later):** *Why the failure mode is everywhere.* Four reasons (back office, visible savings, slow process, commercial naïveté). Not yet drafted; raw material exists in conversation notes.

### Infrastructure (post-launch)
- Add Plausible analytics ($9/mo) plus RB2B free tier for visitor identification
- Reconcile older Four Principles framing in the business plan with the new Three Principles on the site
- Pario legal structure conversation (subsidiary vs. DBA) — separate from website work

### LinkedIn blitz (separate workstream)
- Build a content calendar of ~12 posts, mix of series and standalone
- Series 1: split flagship essay into 3 LinkedIn posts (one per Tax)
- Series 2: shopping list analogy (new content, 3–4 posts with AI-generated imagery)
- Series 3: failure-mode-everywhere series (4 posts)
- Each series links back to the Acuity site for full context

### Future considerations
- Migrate to Next.js when nav/CSS duplication becomes painful
- Add a Writing index page when there are 3+ essays to organize
- Add an asset refresh program / case study deep page if portfolio grows

---

## 9. Code artifacts (latest local versions)

The following are the *intended* current state of each file, reflecting all updates made through the latest edit session. The **deployed version is older** and should be replaced with these versions to bring the live site to spec.

### vercel.json

```json
{
  "cleanUrls": true,
  "trailingSlash": false
}
```

### File: index.html

This is the home page. It contains, in order: nav, hero, stats strip, origin story, principles, what I do (Acuity + Pario cards), Pario dedicated section, selected work (3 teasers), writing (1 essay card), contact, footer.

The full file is approximately 600 lines and uses embedded CSS. Rather than inlining the entire file here, the canonical version exists in the repository at `index.html`. **Key sections that differ from the deployed version:**

**Principles section (markup):**

```html
<section class="principles" id="principles">
  <div class="container">
    <span class="section-label">Principles</span>

    <div class="principle">
      <div class="principle-num">01</div>
      <div class="principle-content">
        <h3>Early is the only leverage.</h3>
        <p>Eighteen months of runway is a strategy. Sixty days is a transaction. Vendors have quarter-end, year-end, and pipeline pressures that are mostly invisible to buyers, and a credible commitment to close on their timing can move a price no amount of negotiation will. Either way, time is the instrument. You have to know how to use it.</p>
      </div>
    </div>

    <div class="principle">
      <div class="principle-num">02</div>
      <div class="principle-content">
        <h3>Information is currency. Spend it intentionally.</h3>
        <p>Vendors are trained to extract information. Budget, timeline, internal politics, pain points. Buyers are almost never trained to withhold it. Every piece you share moves the price, narrows your options, or shifts a deadline. The discipline isn't silence. It's knowing what each piece is worth before you spend it.</p>
      </div>
    </div>

    <div class="principle">
      <div class="principle-num">03</div>
      <div class="principle-content">
        <h3>Right price is determined, not discovered.</h3>
        <p>Requirements are the only thing that tells you what a piece of software is worth to you. Benchmarks tell you what other companies paid. Vendor quotes tell you what they hope you'll pay. Neither of those is an answer. Your requirements are.</p>
      </div>
    </div>
  </div>
</section>
```

**Principles section (CSS):**

```css
.principle-num {
  font-family: 'Inter', sans-serif;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.15em;
  color: var(--accent);
  line-height: 1;
  padding-top: 12px;
}
.principle-content h3 {
  font-family: 'Inter', sans-serif;
  font-size: 22px;
  font-weight: 600;
  letter-spacing: -0.01em;
  line-height: 1.3;
  margin-bottom: 16px;
  color: var(--ink);
}
```

**Card mirroring fix (CSS):**

```css
.card {
  background: var(--paper);
  border: 1px solid var(--rule);
  padding: 48px 40px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.card h3 {
  font-size: 24px;
  font-weight: 600;
  letter-spacing: -0.015em;
  margin-bottom: 20px;
  min-height: 60px;
}
.card-body {
  font-size: 15px;
  line-height: 1.6;
  color: var(--ink-soft);
  margin-bottom: 24px;
  flex-grow: 1;
}
.card-for {
  font-size: 14px;
  color: var(--ink-muted);
  line-height: 1.55;
  border-top: 1px solid var(--rule);
  padding-top: 20px;
  margin-bottom: 28px;
  min-height: 80px;
}
```

**Body font (CSS, applies globally):**

```css
body {
  background: var(--bg);
  color: var(--ink);
  font-family: 'Inter', -apple-system, sans-serif;
  font-size: 18px;
  line-height: 1.6;
}
```

**Italic emphasis (CSS, all em tags within section headlines):**

The pattern across all section headings is: `<h2>The deals were different every time. <em>The failure mode was the same.</em></h2>`. The `em` tag should render as plain text in accent color, no italic:

```css
em { color: var(--accent); font-style: normal; font-weight: inherit; }
```

The only exceptions are:
- `.nav-logo em` — keeps Fraunces italic for the wordmark "Sourcing"
- `.article em` — inside the essay body, retains Fraunces italic for inline prose emphasis

### File: about.html

Origin story page. Long-form first-person narrative covering: childhood/Integrity Auto opener → career chapters at Macmillan, Moody's, Fed, BlackRock, GE Vernova → consolidating thesis → Acuity and Pario as the response.

Key style notes:
- Max content width 780px (narrower than home for readability)
- Photo block at top with placeholder ("JV" initials) — replace with real photo
- Bridge paragraph (`p.bridge`) uses left border accent and increased font weight
- Closing thesis paragraph (`p.thesis`) uses left border accent

### File: work.html

Selected Work / Portfolio. Seven anonymized case studies in *situation → approach → outcome* format. Two-column layout: case meta (industry, title, deal description) sticky on the left, body text on the right. Stacks at 820px breakpoint.

Cases (in order):
1. Newly Independent Global Technology Company — Spin-off Separation, $750M Engineering Apps Portfolio (GE Vernova, anonymized)
2. Global Asset Management Firm — Trading Platforms and M&A Integration, $85M Annual Spend (BlackRock, anonymized)
3. Global Financial Analytics Firm — Post-Audit ITAM Program Buildout, $500M+ in Software Assets (Moody's, anonymized)
4. Global Financial Analytics Firm — Microsoft Enterprise Agreement During M&A Growth (Moody's, anonymized)
5. Global Publisher — Procure-to-Pay System Buildout, $1M First-Year Savings (Macmillan, anonymized)
6. Global Asset Management Firm — Proportional Vendor Onboarding for High-Velocity Category (BlackRock, anonymized)
7. Central Bank Research Institution — Sourcing Policy Training Program (Fed NY, anonymized)

### File: how-i-work.html

Services / engagement models. Three primary services:

1. **Requirements Development** — for teams at the front end of a purchase
2. **Competitive Bid Design** — for teams running an active RFP
3. **Deal Strategy and Negotiation Support** — for teams approaching a major purchase or renewal

Plus two closing sections: "Other capabilities" (acknowledging adjacent work without leading with it) and "How engagements are structured" (project-based, retainer, day rate; intake process).

### File: writing/software-expensive.html

The flagship essay: *"Your software isn't expensive because the code is heavy. It's expensive because you don't know how to buy it."*

Length: ~1,200 words. Structure:
- Setup: software pricing is fundamentally different from commodity pricing
- Reframe: cost-to-service, labor variability, hidden margin
- Pivot: 20 years on the buyer's side, the same pattern at every company, three "taxes"
- Section 1: The Requirements Tax
- Section 2: The Attention Tax
- Section 3: The Leverage Tax
- Closer: What the three have in common; right price is determined by requirements

Style notes:
- Drop cap on the first paragraph (large green letter, Inter 700 weight)
- Section dividers: 40px green underline above each h2
- Max width 680px for readability
- Byline: "Jake Vigneri", date, read time

---

## 10. Voice and content guidelines

When generating new content for this site (essays, case studies, page revisions):

1. **First person, always.** "I" not "we." Acuity is one person.
2. **No em dashes.** Use commas, periods, or restructure the sentence.
3. **Confident observer tone.** When pointing out buyer mistakes, frame as patterns (the system, the situation) rather than accusations (you).
4. **No absolutes.** Avoid "always," "every," "never." Use "most," "often," "usually."
5. **Concrete numbers over abstractions.** "$85M annual spend" beats "significant spend."
6. **Practitioner language.** "The deal," "the table," "the buyer's side," "the work." Avoid "leveraging synergies" or any consultancy-speak.
7. **Short sentences for emphasis.** "Discovery isn't free. It's deferred." Punchy fragments are welcome.
8. **No exclamation points.** No emoji in body text or headlines.
9. **No questions to the reader.** Don't end paragraphs with "What do you think?" — that's LinkedIn voice, not site voice.
10. **Anonymize client work** when describing past engagements. Industry + deal shape, not company name.

---

## 11. Source material and assets

The following live in user-data uploads or were referenced during the project:

- `Acuity_Sourcing_Business_Plan.docx` — full business plan; older Four Principles framing in here, needs reconciliation
- `JV_Acuity_Bio_and_Articles_v2.docx` — biographical material
- `J_Vigneri_Resume_Oct25.docx` — full resume with deal-level numbers
- `Acuity_Framework_Proactive_Solution_Resiliance_Program.docx` — PSR program detail (not currently on the site)
- `Acuity_Sales_Tactics_Articles.docx` — vendor sales tactics series, candidates for Essay #3
- `Linkedin_Post_*.docx` (multiple) — existing LinkedIn posts, source material for essay polishing
- `Narrative.docx` — career narrative draft, source for the About page
- `acuity_logo.jpg` — current Acuity logo with blue-teal-green gradient

Pario product code is managed in a separate repository (`jakevig-design/rfp-agent`) and a separate Claude conversation. Not part of this site's scope.

---

## 12. Quick reference — common edits

**Add a new essay:**
1. Create `writing/[slug].html` using `writing/software-expensive.html` as a template
2. Update the home page `Writing` section if it should be featured
3. Push to GitHub; Vercel auto-deploys

**Change a CSS variable globally:**
1. The `:root` block exists in every HTML file. All five files need to be updated.
2. (This is the duplication tax mentioned in Section 2.)

**Update the nav:**
1. The nav block is duplicated across all five pages. Change all five.
2. Watch for the `current` class — each page has its own nav link marked as `current`.

**Add a new portfolio case:**
1. Edit `work.html`. Add a new `<div class="case">` block following the existing pattern.
2. Optionally update the home page's Selected Work teasers if the new case is feature-worthy.

---

End of handoff document.
