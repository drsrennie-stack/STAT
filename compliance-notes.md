# STAT Success Workbook - Accessibility & Compliance Notes

**Project:** STAT Success Workbook, Edition 2 (exam-by-exam "Stage" structure)
**Files covered:** `STAT_Success_Workbook_v2.pdf` (55 pages, US Letter, single-file print-ready). Companion `hub.html` (restructured June 12, 2026). `stat-acuity-quick-check.html` (Addendum A). Internal review tool `v2-review/review.html` (Addendum B).
**Build script:** `build/build_workbook.py` (ReportLab, brand TTFs embedded from `build/fonts/`)
**Date:** June 12, 2026 (Edition 2 pre-release audit)
**Reviewer:** Dr. Sharilyn Rennie / build pipeline auto-audit

**Structure (55 pages):**

- Front matter (6 pages): cover, copyright, welcome, a note on failure, how to use, contents
- Part 1 Triage (12 pages): divider, three acuities, grade audit, diagnostic intro, 4 dimension pages, scoring, interpretation, decision flowchart, stabilize first
- Part 2 How to Study (8 pages): divider, Recall Toolbox intro, six technique pages
- Part 3 The Stage (14 pages): divider, how a Stage works, 4 Stage worksheet sets (Analyze, Decide, Reanalyze)
- Case Library (9 pages): divider, index, seven cases (Morgan, Jordan, Alex, Riley, Sam, Casey, Taylor)
- Part 4 After STAT (6 pages): divider, discharge planning, rebound vs prevention, warning signs, quick reference, back cover

---

## 1. Standard & target level

| Standard | Target | Notes |
|----------|--------|-------|
| WCAG 2.2 | AA (PDF print baseline) | Static printable PDF, not a fillable web form. Web-specific criteria (1.4.10 reflow, 2.1.1 keyboard) scoped out by medium. |
| PDF/UA | Partial | The build does not embed structural tags. Carried over as a known limitation from Edition 1. See remediation. |
| Print contrast | AAA target where achievable (7:1 normal text) | Verified below. |
| Fillable affordance | Print + pencil | Write-in surfaces are pre-printed lines with visible rules. No PDF form fields. |

---

## 2. Color contrast audit (Edition 2 build)

WCAG 2.1 contrast formula. Computed June 12, 2026 from the hex values in `build/build_workbook.py`.

| Text color | Background | Ratio | Pass? |
|------------|-----------|-------|-------|
| Navy `#142A40` body | White `#FFFFFF` | 14.63:1 | AAA |
| Navy `#142A40` body | Off-white `#FAFAF9` | 14.01:1 | AAA |
| Navy `#142A40` | Navy-tint fill `#ECEFF4` | 12.70:1 | AAA |
| Terra-dark `#A0522D` eyebrows | Off-white `#FAFAF9` | 5.38:1 | AA (normal text) |
| Gray `#6B7280` footers, prompts | White | 4.83:1 | AA (normal text) |
| White | Navy `#142A40` (dividers, back cover) | 14.63:1 | AAA |
| Navy-tint text `#C7D2DC` | Navy `#142A40` (divider notes) | 9.53:1 | AAA |
| Gold-bright `#D4AC65` | Navy `#142A40` (divider accents) | 6.89:1 | AA (AAA large) |
| Gold-bright `#D4AC65` | Navy-deep `#0B1B2D` (divider band) | 8.18:1 | AAA |
| White | Stable green `#3E7C52` (acuity pill, 12pt bold) | 4.99:1 | AA normal, passes large-text AAA |
| Navy `#142A40` | Urgent amber `#D49A2E` (acuity pill) | 5.90:1 | AA (large-text AAA) |
| White | Critical red `#BC3B2C` (acuity pill) | 5.53:1 | AA (large-text AAA) |
| White | Crisis deep red `#7E2A22` (acuity pill) | 9.37:1 | AAA |

**Improvement over Edition 1:** the Urgent band now uses navy text on amber instead of white on gold, raising it from 3.10:1 (AA large only) to 5.90:1. No remaining pair sits below 4.5:1.

**Color-only encoding:** none. Every acuity pill carries its written name; score bands carry number ranges and names.

---

## 3. Typography (Edition 2 build)

| Aspect | Status |
|--------|--------|
| Brand fonts embedded | Plus Jakarta Sans (Regular, Medium, SemiBold, Bold, ExtraBold), DM Sans (Regular, Medium, Bold), Lora (Regular, Italic, MediumItalic) subset-embedded as TTF. Resolves Edition 1 known limitation 4. |
| Minimum body size | 9pt (card labels); 10.5pt+ running body; 12pt+ headers. |
| Italic body text | Lora italic for pull-quotes and usage notes only, never bulk copy. |
| All-caps text | Short eyebrow labels and divider tags only. |
| Underlines | Not used. |

---

## 4. Structural & navigational accessibility

| Element | Status |
|---------|--------|
| Page numbers | Present on every numbered content page. Cover, dividers, and back cover intentionally omit. |
| Section markers | Eyebrow text on every page identifies part and section. |
| Table of contents | Page 6. Lists all parts and the Stage cycle. |
| Stage predictability | Every Stage set repeats the identical three worksheets (Analyze, Decide, Reanalyze) in the same order, a deliberate cognitive-load reduction for overwhelmed readers. |
| Quick reference | Page 54. Summarizes the acuities, failure modes, and the Stage cycle. |
| Reading order | Strict top-to-bottom, left-to-right. No multi-column body text. |
| QR codes | Pages 9 and 10 (Grade Audit, Failure Mode Diagnostic) link to the matching hub tools. QR boxes carry written URLs as the non-scannable fallback. |

---

## 5. Print + reader compatibility

| Test | Result |
|------|--------|
| Page size | 8.5 x 11" (Letter). |
| Margins | Safe for home printers, no trim bleed required. |
| Ink budget | Dividers and back cover are full-bleed navy (5 pages of 55). Body pages are near-zero ink. |
| File size | 229 KB (font embedding accounts for the increase over Edition 1's 103 KB). Email-friendly. |

---

## 6. Companion hub (`hub.html`, restructured June 12, 2026)

The hub was reorganized to mirror Edition 2: Part 1 Triage, Part 2 How to Study, Part 3 The Stage, Case Library, Part 4 After STAT, plus an Edition 1 archive section that keeps every week-by-week tool reachable for original-edition buyers. Terminology pass applied (recovery becomes rebound, weeks become Stages, second person throughout). **Tool filenames and URLs are unchanged**, so QR codes printed in sold Edition 1 workbooks continue to resolve.

Carried-over accessibility features, re-verified in the restructure: skip link, semantic landmarks and heading hierarchy, visible 3px gold-bright focus indicators, `prefers-reduced-motion` support, `target="_top"` on internal links, `target="_blank" rel="noopener"` on the one external link, iframe height-sender before `</body>`. New archive list links use the same focus and hover treatments as tool cards.

Contrast on hub pairs is unchanged from the prior audit (all AA or better; navy on white 14.7:1, gold-bright on navy 6.9:1, gray on white 4.8:1).

---

## 7. Known limitations (Edition 2)

1. **No PDF tags / structure tree.** ReportLab canvas output is untagged. Screen-reader users get reading order but no heading levels or landmarks. Remediation: post-process with tagging tooling or migrate to the Platypus story API.
2. **No form fields.** Print-and-pencil remains the chosen mode. A fillable variant remains a bundle add-on candidate.
3. **Decision flowchart long description.** The flowchart is text-labeled but has no separate long description. Carried from Edition 1.
4. **Web tools beyond the hub.** The individual tool pages in the `drsrennie-stack/STAT` repo have not yet received the Edition 2 terminology pass (rebound, Stages, second person). Display copy inside those pages may still say "recovery" and "week." Hub display names were updated; filenames stay frozen.

---

## 8. Remediation plan

| Item | Priority | Target |
|------|----------|--------|
| Terminology pass on individual tool pages in the STAT repo | High | Before semester hand-out |
| Re-upload `hub.html` to the repo (project copy and repo copy must match) | High | Before semester hand-out |
| Tagged-PDF structure (PDF/UA) | Medium | Edition 2.1 |
| Fillable-PDF variant | Medium | Bundle add-on |
| Flowchart long description | Low | Edition 2.1 |

---

## 9. Reviewer sign-off

Edition 2 meets WCAG 2.2 AA for color contrast, typographic legibility, structural navigation, and color-independent encoding in its print-PDF form, and improves on Edition 1 (brand fonts embedded, Urgent pill contrast raised, no pair below 4.5:1). PDF/UA structural tagging remains deferred.

**Pending before sign-off is final:** Dr. Rennie's page-by-page review of `STAT_Success_Workbook_v2.pdf` (see `v2-review/review.html`).

**Reviewer:** Dr. Sharilyn Rennie
**Date:** June 12, 2026

---

## Addendum A. Companion web tool: Acuity Quick Check

**File:** `stat-acuity-quick-check.html` (single-file HTML, CSS and JS inline)
**Purpose:** Four-question triage tool. Sorts a student into Stable, Urgent, or Critical and links onward to the full Failure Mode Diagnostic. Companion to the workbook's acuities page.
**Date added:** May 20, 2026
**Reviewer:** Dr. Sharilyn Rennie / build auto-audit

### A.1 Standard & target level

| Standard | Target | Notes |
|----------|--------|-------|
| WCAG 2.2 | AA achieved; AAA on most pairs | Interactive web tool. Web-specific criteria (keyboard, reflow, focus order, name/role/value) are in scope and verified below. |

### A.2 Color contrast audit

WCAG 2.1 contrast formula. Colors from the PRIMARY palette plus `--gold-bright #D4AC65`.

| Text / element | Background | Ratio | Pass? |
|----------------|-----------|-------|-------|
| Navy `#142A40` body, headings, option text | White `#FFFFFF` | 14.7:1 | AAA |
| Navy `#142A40` selected option text | Navy-tint `#ECEFF4` | 12.7:1 | AAA |
| Gray `#6B7280` help text and byline | White | 4.8:1 | AA (normal text) |
| Terra-dark `#A0522D` eyebrow labels, progress count | White | 5.6:1 | AA |
| White hero h1 | Navy `#142A40` | 14.7:1 | AAA |
| Gold-bright `#D4AC65` hero eyebrow and tagline | Navy | 6.9:1 | AA (AAA for large) |
| White, Stable badge | Navy `#142A40` | 14.7:1 | AAA |
| Navy, Urgent badge | Gold `#B8924A` | 5.1:1 | AA |
| White, Critical badge | Terra-dark `#A0522D` | 5.6:1 | AA |
| Gold-bright footer link | Navy | 6.9:1 | AA |
| Gray-light `#D1D5DB` footer fine print | Navy | 9.9:1 | AAA |

Result acuity is never encoded by color alone: each band carries a written level number and name ("Level 2 · Urgent"). The disabled Continue button (white on gray-light) is exempt under WCAG 1.4.3 (inactive component).

### A.3 Keyboard navigation flow (verified)

Tab order: skip link → Begin button → footer links (intro); progress (not focusable) → radio group → Back → Continue → footer links (question); result CTAs → Start-over → footer links (result). Radio options use native inputs: arrow keys move within the group, Space selects. All buttons operate with Enter and Space. Verified with automated browser testing: keyboard selection enables the Continue button; focus moves to the question legend on each step and to the result heading on completion; Back from question 1 returns to the intro and focuses the Begin button.

### A.4 Screen reader support

Semantic landmarks (`header`, `main`, `footer`), heading hierarchy (h1 → h2 → h3), each question wrapped in `fieldset` with a `legend`, native radio inputs with associated `label` elements. An `aria-live="polite"` region announces every step ("Question 2 of 4...") and the final result. The question legend and result heading carry `tabindex="-1"` and receive programmatic focus on step change so non-visual users land on new content. Decorative elements (progress bar, custom radio mark, arrow glyphs) are `aria-hidden`. Verified programmatically (DOM semantics, ARIA, focus order). Recommended: one manual pass with VoiceOver or NVDA before the QR goes live.

### A.5 Other compliance items

`prefers-reduced-motion` disables all transitions and smooth scrolling. Visible focus indicators (3px gold-bright outline) on every interactive element. Skip link to main content. Responsive from 380px upward (verified). A `noscript` fallback points users to the printed acuity page and the full diagnostic. Internal links carry `target="_top"`; the external `medmasterscollaborative.com` link uses `target="_blank" rel="noopener"`. The iframe height-sender script (postMessage with id, ResizeObserver, load and resize listeners) is baked in before `</body>`.

### A.6 Known limitations and remediation

1. Fonts load from Google Fonts CDN; offline or blocked, the tool falls back gracefully to system sans-serif and serif. No remediation needed.
2. No manual screen-reader pass yet. Remediation: one VoiceOver or NVDA pass before publishing.
3. The quiz requires JavaScript; with JS disabled only the intro and the noscript message show. Acceptable for an interactive tool; the workbook's printed acuity page is the offline equivalent.
4. Not yet hosted. The workbook QR cannot be regenerated until the final live URL is confirmed.

**Reviewer:** Dr. Sharilyn Rennie
**Date:** May 20, 2026

---

## Addendum B. Internal review tool: `v2-review/review.html`

Internal proofing tool (not student-facing, not published). Built June 12, 2026 to support the Edition 2 page-by-page review. Includes skip link, labeled textareas (`for` + `id`), `aria-pressed` toggle buttons, `aria-live` progress count, keyboard-operable image zoom (`dialog`), visible gold focus indicators, `prefers-reduced-motion` support, alt text on every page image, and the iframe height-sender. Marks persist in browser localStorage; the Export button produces `v2-review-notes.md` containing only flags and notes, no student data.

---

## Appendix. Edition 1 audit (superseded)

The Edition 1 audit (May 19, 2026, covering the 66-page `STAT_Success_Workbook.pdf`) is superseded by this document. Edition 1 shipped at WCAG 2.2 AA with two pairs at AA-large-only (Urgent and Critical pills) and Helvetica/Times placeholder fonts. Both issues are resolved in the Edition 2 build. The original v1 files (`STAT_Success_Workbook.pdf`, `STAT_Success_Workbook_original.pdf`) remain in the project folder unchanged.
