# Design Review: book-6-security-architecture.html
**Date:** 2026-08-18
**Reviewer:** multi-persona-design-review (ZCode)
**Severity threshold:** medium
**Parent run:** Agent 01 brochure generation (first production run)

## Summary

The brochure passes structural verification (8/8 checks) but fails the quality gate. Four personas identified 7 HIGH findings requiring resolution before publish. The most critical issues are a fabricated "5x" cost statistic (Architect), a placeholder ASIN in the Buy link (Sales Adviser), cliché heading phrasing (Editor), and missing purchase CTAs in the body flow (Sales Adviser). The visual design system is sound — no HIGH findings from the Artist.

**Pass/Fail Gate: ❌ FAIL — 7 HIGH findings require resolution before publish.**

---

## Principal Architect Review

| Severity | Location | Finding | Action |
|----------|----------|---------|--------|
| HIGH | Insight 03 body | Fabricated "5x" cost statistic with no source — recognizable trope that destroys credibility with practitioners who run PCI remediation programs | Replace with defensible qualitative statement grounded in real mechanism (DTMF suppression, recording redaction, scope-reduction) |
| HIGH | Hero sub | "SRTP enforcement patterns" mischaracterizes architect control — SRTP is enforced by default on Genesys Edge, not an architect-selected pattern. Points at wrong control for PCI/HIPAA audits | Replace with actual audit-determining controls: DTMF suppression, payment scope isolation, recording redaction, Edge trust boundary design |
| MEDIUM | Insight 01 body | "Most contact center security breaches" is an unattributed quantitative claim — no public dataset supports "most" for contact centers specifically | Soften to attributable pattern: "Contact center breaches routinely exploit assumed trust between internal services" |
| MEDIUM | Insight 02 body | "Genesys Cloud, AWS, and hybrid" is a confused triad — Genesys Cloud IS hosted on AWS; listing them as separate targets suggests the author doesn't know this | Rewrite: "Genesys Cloud (multitenant), customer-owned AWS workloads integrating via Platform API, and Genesys Cloud CX Edge on-premises" |
| MEDIUM | Insight 03 body | "Specific patterns for each regulation" is an overbroad promise — PCI-DSS alone has ~300 sub-requirements; each regulation is book-length | Narrow to "control families most often cited in contact center audits" and surface one named pattern |
| MEDIUM | Chapter preview | No Genesys-specific substance — indistinguishable from any generic zero-trust management book. Mentions no OAuth, SCIM, role inheritance, Edge certificates, or BYOC SIP security | Inject at least one Genesys-grounded concrete element into the preview |
| MEDIUM | Author bio | "15 years" tenure + "Principal Genesys Cloud CX Architect" implies 15 years of Genesys Cloud specifically — impossible since PureCloud GA was ~2014-2017 | Disambiguate: "15 years across enterprise contact center platforms including Genesys Engage/PureConnect on-prem and Genesys Cloud CX" |
| LOW | Numbering | Two colliding numbering schemes: "Trilogy Vol. I" and "Other Books Vol. 1-4" | Pick one scheme; rename the other-book labels to avoid two different "Vol. I" books |
| LOW | Author creds | No Genesys-specific certification (GCSA) or security credential (CISSP) despite the topic | Surface a Genesys or security credential if held; soften authority posture if not |

---

## Editor Review

| Severity | Location | Finding | Action |
|----------|----------|---------|--------|
| HIGH | Insight 03 heading | "Built In, Not Bolted On" is one of the most worn phrases in enterprise tech writing — signals filler before reader reaches real content | Replace with specificity-led heading: "Compliance Is an Architecture Constraint, Not a Remediation Project" |
| HIGH | Insight 02 body opening | Opens with architectural description ("In a multi-cloud...") rather than reader's pain. Pain is: you can no longer draw a defensible perimeter | Rewrite: "You can no longer point to a perimeter and say 'this is where the contact center is defended.'" |
| HIGH | Insight 03 body opening | Passive voice ("are treated") in opening position + "when they should be" lectures reader. Strongest asset (cost stat) buried mid-card | Lead with cost pain in active voice (if stat is sourced) or drop stat and lead with mechanism |
| MEDIUM | Section title | "Three Insights That Change How You Think" — vague marketing language promising transformation without substance | Replace with concrete promise: "Three Decisions That Determine Whether Your Contact Center Passes Audit" |
| MEDIUM | Section sub | Repeats "audit checkbox" trope already used in Insight 03 — conceptual repetition within one scroll degrades practitioner voice | Rewrite to carry distinct information: "Frameworks validated across enterprise deployments that survived both breach attempts and regulator review" |
| MEDIUM | Lead magnet subhead | Purely transactional ("Enter your email and we will send") with zero benefit framing | Rewrite to anchor on payoff: "Get the full Chapter 1 — the zero trust maturity model, decision-rights framework, and access-control pattern" |
| MEDIUM | Chapter preview para 3 | "This chapter introduces" is process narration, weakest way to open closing paragraph. Leans on "reactive firefighting → structured discipline" cliché | Lead with deliverable and its effect: "A zero trust maturity model gives you named decision rights, explicit service-level ownership..." |
| MEDIUM | CTA button text | "Send Me Chapter 1 →" is functional but flat — centers author's action rather than reader's gain | Sharpen: "Get Chapter 1 Free →" or "Read Chapter 1 Free →" |
| LOW | Insight 01 opening | Double-negative construction ("not because X but because Y") slows opening; "trust was assumed" is passive in load-bearing position | Tighten: "Most contact center breaches happen because internal services trusted each other by default" |
| LOW | Hero sub closing | "survives audit or fails it" is slightly melodramatic; "or fails it" tag redundant | Trim: "whether your deployment passes audit" |
| LOW | Chapter preview para 2 | "is rarely the bottleneck" sits passively where stakes should tighten | Optional: "something else becomes the bottleneck" |

---

## Sales Adviser Review

| Severity | Location | Finding | Action |
|----------|----------|---------|--------|
| HIGH | Nav + Footer | Buy link points to placeholder ASIN `B0TEST1234` — purchase path is broken end-to-end. Launch blocker | Replace with live ASIN before any traffic is sent |
| HIGH | Body flow | No "Buy on Amazon" CTA anywhere in the body. Desire is built well (insights → preview → email ask) but never converted to a sale. Lead captured but no purchase path | Insert primary "Buy on Amazon" button after lead-magnet section; optionally a second after chapter preview |
| MEDIUM | Lead magnet offer | Specific about *what* and *when* but not *format*, *length*, or *what reader can do after* | Add: "a 12-page PDF you can apply before your next architecture review" |
| MEDIUM | Social proof | Zero testimonials, ratings, or named deployment outcomes. For security/compliance audience that buys on trust, gap between insights and preview | Insert practitioner testimonial or concrete deployment result between insights grid and chapter preview |
| MEDIUM | Hero sub | Value promise buried under long descriptive clause. No single sharp outcome promise in first 3 seconds | Lead with one-line outcome promise: "Design a contact center that passes audit the first time" |
| LOW | Free chapter offer | No urgency or scarcity — "Get Chapter 1 Free" with no deadline | Consider light contextual urgency: "Free preview during launch week" (optional) |
| LOW | Other Books grid | Lists only Vol. 1-4, omits book-5 ("Decoding Language"). Also, trilogy companions absent | Add missing sibling; link trilogy companions when available |

---

## Artist Review

| Severity | Location | Finding | Action |
|----------|----------|---------|--------|
| MEDIUM | Hero eyebrow (`.book-eyebrow`) | Dark accent `#1E3A5F` on near-black `#0B1220` gives ~1.6:1 contrast ratio — below legibility threshold. Sibling's teal `#006E7C` reads at ~3.2:1 | For elements on `--dark`, use a lightened accent stop (`--accent-on-dark`) instead of raw midpoint accent |
| MEDIUM | Chapter body | Three flat paragraphs with no `<strong>`/`<em>` emphasis. Sibling book-1 uses editorial emphasis to create scannable focal point. Book-6 reads as gray wall of body text | Introduce one `<strong>`/`<em>` emphasis pair to create visual anchor matching sibling editorial weight |
| LOW | Lead button | Redundant inline `style="color:#1E3A5F"` — CSS already defines `color: var(--accent)`. Sibling omits inline. Family is inconsistent | Standardize: either rely on CSS var in all siblings or add inline hex to all siblings |
| LOW | Spine art on mobile | `display: none` at `max-width: 640px` — spine (book's primary visual identity) vanishes on most common viewport. Shared design decision | Consider compact horizontal spine/cover motif for mobile, or accept as family-wide rule |

**Compliance checks passed:** spine gradient (correct 3-stop), box-shadow (matches spec exactly), insight card accent border (3px, correct), accent-tinted rule lines (correct rgba decomposition).

---

## Prioritized Action List

### HIGH (must fix before publish)

1. **[Architect]** Replace fabricated "5x" cost statistic in Insight 03 — credibility-destroying for practitioners
2. **[Architect]** Replace "SRTP enforcement patterns" in hero sub — technically incorrect; SRTP is Edge-enforced by default, not architect-selected
3. **[Editor]** Replace "Built In, Not Bolted On" heading — worn cliché signals filler
4. **[Editor]** Rewrite Insight 02 opening to lead with reader's pain, not architectural description
5. **[Editor]** Rewrite Insight 03 opening — remove passive voice and lecturing tone
6. **[Sales]** Replace placeholder ASIN `B0TEST1234` with live ASIN — purchase path is broken
7. **[Sales]** Add "Buy on Amazon" CTA button in body flow — desire is built but never converted

### MEDIUM (should fix before publish)

8. **[Architect]** Soften "most contact center breaches" to attributable pattern *(also flagged by Editor)*
9. **[Architect]** Fix "Genesys Cloud, AWS, and hybrid" triad — Genesys Cloud IS on AWS
10. **[Architect]** Narrow "specific patterns for each regulation" — overbroad promise
11. **[Architect]** Add Genesys-specific substance to chapter preview
12. **[Architect]** Disambiguate "15 years" tenure vs Genesys Cloud product history
13. **[Editor]** Replace section title "Change How You Think" with concrete promise
14. **[Editor]** Rewrite section sub to avoid repeating "audit checkbox" trope
15. **[Editor]** Rewrite lead magnet subhead with benefit framing
16. **[Editor]** Rewrite chapter preview para 3 — remove process narration
17. **[Sales]** Add format/length/outcome to lead magnet offer
18. **[Sales]** Add social proof between insights and preview
19. **[Sales]** Lead hero sub with sharp outcome promise
20. **[Artist]** Fix hero eyebrow contrast — use lightened accent on dark backgrounds
21. **[Artist]** Add editorial emphasis to chapter body paragraphs

### LOW (nice-to-have)

22. **[Architect]** Resolve numbering scheme collision (Trilogy Vol. I vs Other Books Vol. 1-4)
23. **[Architect]** Surface Genesys or security credential in author creds
24. **[Editor]** Tighten Insight 01 double-negative opening
25. **[Editor]** Trim "survives audit or fails it" melodrama
26. **[Sales]** Add light urgency to free chapter offer
27. **[Sales]** Add missing book-5 to Other Books grid
28. **[Artist]** Standardize inline color convention across siblings
29. **[Artist]** Consider mobile spine art alternative

---

## Pass/Fail Gate

**❌ FAIL — 7 HIGH findings require resolution before publish.**

The brochure passes structural verification (8/8 automated checks) but fails the human-judgment quality gate. The HIGH findings cluster around two themes:
1. **Credibility** — fabricated statistics and technically incorrect claims that a senior practitioner would catch immediately
2. **Conversion** — broken purchase path (placeholder ASIN) and no purchase CTA in the body flow

Both themes must be resolved before this brochure goes live.

---

## Human Review Feedback (for completion after review)

- [ ] Finding 1 (5x stat): [ ] Valid  [ ] Invalid  [ ] Severity wrong
- [ ] Finding 2 (SRTP): [ ] Valid  [ ] Invalid  [ ] Severity wrong
- [ ] Finding 3 (cliché heading): [ ] Valid  [ ] Invalid  [ ] Severity wrong
- [ ] Finding 4 (Insight 02 opening): [ ] Valid  [ ] Invalid  [ ] Severity wrong
- [ ] Finding 5 (Insight 03 opening): [ ] Valid  [ ] Invalid  [ ] Severity wrong
- [ ] Finding 6 (placeholder ASIN): [ ] Valid  [ ] Invalid  [ ] Severity wrong
- [ ] Finding 7 (no purchase CTA): [ ] Valid  [ ] Invalid  [ ] Severity wrong

Overall accuracy: ___% | False positive rate: ___%

Save feedback to: `C:\Research Tasks\agent-logs\multi-persona-design-review\feedback\book-6-review.json`