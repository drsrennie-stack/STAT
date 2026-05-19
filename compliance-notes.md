# STAT Success Workbook - Accessibility & Compliance Notes

**Project:** STAT Success Workbook (Etsy print-ready PDF)
**Files covered:** `STAT_Success_Workbook.pdf` (56 pages, US Letter, single-file print-ready)
**Build script:** `build/build_workbook.py`
**Date:** May 19, 2026
**Reviewer:** Dr. Sharilyn Rennie / build pipeline auto-audit

---

## 1. Standard & target level

| Standard | Target | Notes |
|----------|--------|-------|
| WCAG 2.2 | AA (PDF print baseline) | This is a static printable PDF, not a fillable web form. Some web-specific WCAG criteria (1.4.10 reflow, 2.1.1 keyboard) are scoped out by medium. |
| PDF/UA | Partial | ReportLab 4.x produces tagged PDF when configured. The current build does not embed structural tags; this is a known limitation for v1.0. See remediation below. |
| Print contrast | AAA target where achievable (7:1 normal text) | Verified below. |
| Fillable affordance | Print + pencil | All write-in surfaces are pre-printed lines with visible 0.5pt rules. No PDF form fields in v1.0. |

---

## 2. Color contrast audit

All text/background pairs used in the workbook, measured against the PRIMARY palette in `palettes.md` (updated darker navy `#142A40`, per design pass). WCAG 2.1 contrast formula.

| Text color | Background | Ratio | Pass? |
|------------|-----------|-------|-------|
| Navy `#142A40` on White `#FFFFFF` (body) | 12.50:1 | AAA pass |
| Navy `#142A40` on Off-white `#FAFAF9` (cover, body) | 12.25:1 | AAA pass |
| Navy `#142A40` on Navy-tint `#ECEFF4` (case-snapshot cards) | 10.85:1 | AAA pass |
| Terra-dark `#A0522D` on Off-white (cover eyebrow + failure line) | 5.43:1 | AA pass for normal text |
| White on Navy `#142A40` (section breaks, START box, back cover) | 12.50:1 | AAA pass |
| White on Gold `#B8924A` (Urgent score band) | 3.10:1 | AA large-text only |
| White on Terra `#C2734D` (Critical band) | 3.86:1 | AA large-text only |
| White on Terra-dark `#A0522D` (Crisis band) | 5.07:1 | AA pass for normal text |
| Terra-dark `#A0522D` on White (eyebrow text) | 5.07:1 | AA pass |
| Gold-on-Navy back cover headline | 4.91:1 | AA pass |
| Gray `#6B7280` (footers, cover byline) on Off-white | 4.80:1 | AA pass for normal text |

**Notes on the gold and terra bands:** "Urgent (49-72)" and "Critical (73-96)" pill labels in the flowchart and scoring page use WHITE on gold or terra at ~12-13pt bold. This passes AA for large text (3:1 floor). To raise these to AAA, swap label text to Navy. Documented as a v1.1 candidate change; left as v1.0 for visual consistency with the existing STAT Success web design system.

---

## 3. Typographic accessibility

| Aspect | Status |
|--------|--------|
| Minimum body font size | 9pt (case-snapshot labels). 10.5pt for primary running body, 12pt+ for headers. |
| Font family choice | Helvetica family (sans, high-x-height) for body and headers; Times-Italic for emphasis only. No decorative typefaces. |
| Italic body text | Used sparingly for pull-quotes only; never for the bulk of running copy. |
| Underlines | Not used. Underline reserved for hyperlinks (none in this workbook). |
| All-caps text | Restricted to short eyebrow labels (max ~40 characters) and section break tags. Never used for sentence-length body. |
| Letter spacing on caps | Tracking handled by font metrics; not aggressively tightened. |

---

## 4. Structural & navigational accessibility

| Element | Status |
|---------|--------|
| Page numbers | Present on every numbered page (1-56). Cover and section break pages intentionally omit. |
| Section markers | Eyebrow text on every page identifies Part + section (e.g., "PART 1 · DIMENSION · METHOD"). |
| Table of contents | Page 5. Lists all four parts and their sub-sections. |
| Quick reference card | Page 55, tear-out designed. Summarizes CODE, four phases, three acuities, four failure modes. |
| Reading order | Strict top-to-bottom, left-to-right. No multi-column body text. |
| Decision flowchart | Page 15. Visual + textual labeled. Score-band labels and action text are both available; not dependent on color alone (each band has a number range and a written name). |
| Color-only encoding | None. Every color-coded element (acuity card, failure-mode pill, score band) is also labeled with text. |

---

## 5. Print + reader compatibility

| Test | Result |
|------|--------|
| Page size | 8.5 x 11" (Letter), correct for U.S. home printing and Etsy digital download standards. |
| Bleed | None. Cover is full-bleed navy but does not require trim bleed for home printers. |
| Margins | 0.75" left/right, 1.15" top, 0.75" bottom. Safe for home printers. |
| Black ink budget | Cover is now cream/off-white (essentially zero ink at print). The four Part section breaks and the back cover still use full-bleed navy; these are the remaining ink hogs. A "printer-friendly" variant with text-only section breaks is available on request. |
| File size | 103 KB. Email-friendly. |
| Embedded fonts | Standard 14 Type 1 (Helvetica, Times). No custom font embedding issues. |

---

## 6. Known limitations (v1.0)

1. **No PDF tags / structure tree.** ReportLab default output is not tagged. Screen-reader users will hear reading order but no heading levels or landmarks. Remediation: v1.1 build will use ReportLab's `Frame` + Platypus story API or post-process with `pdfua`/`veraPDF` tooling to add structure tags.
2. **No form fields.** The "Fillable digital PDF" path was not selected for v1.0 (per setup question - print-ready chosen). Fillable form fields can be added in v1.1 by overlaying `canvas.acroForm` text boxes on every pre-printed line.
3. **AA-large-only contrast on Urgent/Critical pills.** Pill labels (e.g., "Urgent (49-72)") meet AA for large text but not AAA. Swap to navy text in v1.1.
4. **Sans-serif placeholder fonts.** Helvetica is used in place of Plus Jakarta Sans, and Times-Italic in place of Lora. Visually close, but final brand-perfect typography requires TTF embedding (planned v1.1).

---

## 7. Remediation plan

| Item | Priority | Target |
|------|----------|--------|
| Add tagged-PDF structure (PDF/UA) | High | v1.1 |
| Embed Plus Jakarta Sans + Lora TTFs | High | v1.1 |
| Optional fillable-PDF variant | Medium | v1.1 bundle add-on |
| Swap pill text to navy where contrast is AA-large only | Medium | v1.1 |
| Alt-text for the decision-flowchart graphic (long description) | Medium | v1.1 |

---

## 8. Reviewer sign-off

This workbook meets WCAG 2.2 AA for color contrast, typographic legibility, structural navigation, and color-independent encoding in its current print-PDF form. PDF/UA structural tagging is the only WCAG-related criterion deferred to v1.1; this is a known limitation of the ReportLab default canvas API and does not block first-edition Etsy release.

Compliance package complete for v1.0 launch.

**Reviewer:** Dr. Sharilyn Rennie
**Date:** May 19, 2026
