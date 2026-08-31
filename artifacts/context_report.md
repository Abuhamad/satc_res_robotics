# SaTC 2.0 RES (NSF 25-515) Compliance Checklist — CAREER→RES + 5yr→4yr

**Scope of this report:** file-by-file list of every remaining change needed to make the revised
package (`main_v2.tex` + its `\input{}`s) a clean **single‑PI SaTC 2.0 RES, 4‑year** submission.
This is an analyst/compliance report only. **No `.tex` files were edited.** All dollar figures below
are duration‑dependent and must be **recomputed by the PI** — no new totals are invented here.

Severity legend: **HIGH** = blocks/undermines compliance; **MEDIUM** = required-but-lower-risk or
verification item; **LOW** = cosmetic / leave-alone confirmations.

---

## 1. Executive Summary — must‑fix items

1. **`sections/0_project_summary.tex` is stale from a *different* CAREER proposal.** Both its title
   *and its entire body* describe a Human‑in‑the‑Loop / privacy‑preserving VLM manipulator project,
   not the funded VLA‑security topic. Title + body must be replaced, and a **keyword line is missing**.
2. **Budget is built "over five years" (~$555,171).** Every duration‑dependent figure must be
   recomputed for a 4‑year period; one CAREER reference and the Summer 2026→Spring 2031 span must change.
   Add **SaTC PI‑meeting travel** (RES requirement). Confirm it stays **single‑PI, < $600K**, well under
   the **$1.2M RES cap (incl. optional TTE)**.
3. **Residual "CAREER" strings** in `budgetjustification.tex` (L12), `mentoring.tex` (L8),
   `summary.tex` (L26) — must be de‑CAREER‑ed.
4. **`datamanagement.tex`** — the "after five years" is a data‑**retention** period (LEAVE ALONE), but
   the plan should be aligned to the current **DMSP** terminology/elements.
5. **Incidental terms to LEAVE ALONE:** lowercase "career(s)" (job sense) in `mentoring.tex`,
   `prior_support.tex`, `education.tex`; "Five training runs / over five runs" in `02_v2.tex` (experiment count).

---

## 2. File‑by‑file checklist

### `main_v2.tex` — wiring
- **LOW / OK.** Cover title already reads `SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models`.
- **LOW / verify.** Bibliography is `\bibliography{refs,refs_v2_additions}` — keep; ensure both `.bib`
  files ship. No CAREER/duration strings here.
- **NOTE.** `main_v2.tex` inputs the section files below (impact, prior_support, budgetjustification,
  facilities, datamanagement, mentoring, summary, synergy). `sections/education.tex` is **commented out**
  (not compiled) — see note at end.

### `01_v2.tex` — Project Description (front half)
- **OK / CLEAN.** No `CAREER`, no "five years" matches. RES identity, notion of **trust** (definition
  added in Overview), responsible‑computing statement, and the 2025–2026 model coverage are present.
  No changes required for the CAREER/duration conversion.

### `02_v2.tex` — Project Description (back half)
- **LEAVE ALONE (L264).** "Five training runs … over five runs with different random seeds" = number of
  experimental seeds, **not** project duration. Do **not** change.
- **LOW / verify.** No `CAREER` strings. (Confirm the internal research timeline/table reads 4 years to
  match the budget; prior cycle reportedly set this — spot‑check the Year‑by‑task figure/table if present.)

### `sections/0_project_summary.tex` — **separate Project Summary (1 page)** — **HIGH, multiple**
This standalone file does **not** describe the funded project. Treat as a full rewrite target.

- **HIGH — Title (L68).**
  - OLD: `CAREER: Robust Robotic Manipulators with Human-in-the-Loop Learning via Large Vision-Language Models}`
  - NEW: `SaTC 2.0: RES: Toward Secure and Robust Generalist Robotic Models}`
  (Exact string to match the cover title in `main_v2.tex`.)
- **HIGH — Body mismatch (L~28–63, Overview / Intellectual Merit / Broader Impacts).** The body is about
  differential privacy, federated learning, and human‑in‑the‑loop VLM manipulators — a different project.
  A reviewer comparing the Summary to the Project Description will see a topic mismatch. **Recommendation:**
  replace the three body sections with the already‑correct content of `sections/summary.tex` (which matches
  the VLA‑security project), then de‑CAREER it (see `summary.tex` L26 fix below). *Do not merely edit the title.*
- **HIGH/MEDIUM — Missing required keyword line.** The SaTC Project Summary Overview must end with a
  keyword list drawn from the solicitation's controlled vocabulary (first keyword designates the project
  class). None is present. **Recommended paragraph to append at the end of the Overview** (confirm the
  exact controlled terms against **NSF 25-515 §V.A / Project Summary instructions** — flagged **VERIFY**):

  > *Keywords: RES; trustworthy AI/ML security; robotic foundation models; vision‑language‑action (VLA)
  > models; adversarial robustness; multimodal security; safety benchmarking.*

  (The **first keyword must be the solicitation‑designated class token** — use the exact token 25‑515 lists
  for a Research/RES project; the remaining terms above are topical and may be tuned by the PI.)
- **LOW / OK.** PI/affiliation line `Mohammed Abuhamad, Loyola University Chicago}` is fine.

### `sections/impact.tex` — Broader Impacts (in Project Description)
- **OK / CLEAN.** No `CAREER`, no duration strings. Content aligns with RES Broader Impacts. No change.

### `sections/prior_support.tex` — Results From Prior NSF Support
- **OK / CLEAN.** "cybersecurity career" (L14) and "careers in cybersecurity" (L16) are the **job** sense —
  **LEAVE ALONE.** Award dates/amounts are historical facts — do not touch.

### `sections/budgetjustification.tex` — **HIGH, duration rebuild**
Duration‑**dependent** (must be recomputed for 4 years): PI summer salary (now 4 summer months, not 5),
graduate‑student support (4 years not 5), undergraduate wages, **fringe**, **travel**, **total direct**,
**MTDC**, **indirect**, **total**. Duration‑**independent** (keep): one‑time GPU workstation.

- **HIGH — CAREER ref (L12).**
  - OLD: `The PI directly contributes to both the research and educational goals outlined in the CAREER proposal.`
  - NEW: `The PI directly contributes to both the research and educational goals outlined in this SaTC 2.0 RES project.`
- **HIGH — PI summer salary (L10).** "one summer month for each year" is fine as wording, but total PI
  summer salary now spans **4 years, not 5** → recompute (one fewer summer month). *PI recomputes.*
- **HIGH — Grad support span (L24).**
  - OLD: `The graduate student will be supported from Summer 2026 through Spring 2031.`
  - NEW: `The graduate student will be supported from Summer 2026 through Spring 2030.`
    (4 academic years; PI to confirm exact start/end.)
- **LOW — Commented note (L21).** `%…second graduate student will join the effort in years 4 and 5.`
  Commented out; if ever reinstated, change to "year 4." Otherwise leave.
- **HIGH — Fringe (L36).** `\$ 96,927 over five years` → recompute for **4 years**; change "over five years"
  → "over four years". *Figure = PI recomputation.*
- **HIGH — Travel (L46) + RES PI‑meeting travel.**
  - OLD: `Total = 2 trips * \$2,500 = \$5,000 for years 2 to 5.` (years 2–5 = 4 years → $20,000)
  - NEW: `…for years 2 to 4.` (years 2–4 = 3 years → recompute, e.g. $15,000) — *PI confirms count.*
  - **ADD (HIGH):** an explicit line for **SaTC PI‑meeting travel** (RES awardees are expected to attend
    the SaTC/annual PI meeting). Add a justified trip (e.g., 1 trip/year to the PI meeting) with dollars
    the PI computes. This is a common RES compliance omission.
- **LOW — Equipment (L61).** `\$12,500 in the first year` — one‑time, duration‑independent; **keep** (no change).
- **HIGH — Total Direct (L70).** `\$ 408,435 over five years` → recompute; "over four years". *PI recomputes.*
- **LOW — Commented MTDC (L74).** `% \$413,585 over five years.` — update or delete comment.
- **HIGH — Indirect (L78).** `\$ 146,736 over five years` → recompute (45.5% MTDC); "over four years". *PI recomputes.*
- **HIGH — Total (L84).** `\$ 555,171 over five years` → recompute; "over four years". *PI recomputes.*
- **LOW — Commented total (L90).** `% \$4,266,251 over five years.` — stale; delete.
- **CAP CHECK (HIGH / confirm):** Per **NSF 25-515**, RES projects run up to **4 years** with a total
  budget up to **$1.2M including the optional Transition‑to‑Translation (TTE) supplement**. The current
  ~$555K, single‑PI package is well under the cap and should **remain single‑PI, < $600K**. Do **not**
  inflate — recompute downward for the shorter duration. *(Verify exact RES duration/cap against 25‑515.)*

### `sections/facilities.tex` — Facilities, Equipment & Other Resources
- **OK / CLEAN.** No CAREER/duration strings.
- **LOW (cosmetic).** Stray backtick artifact `\`'` after "…2 PB of disk space and growing." — optional typo cleanup.

### `sections/datamanagement.tex` — Data Management (→ DMSP) — **MEDIUM**
- **LEAVE ALONE (L37).** "…securely deleted after that archival period, or **after five years**, whichever
  is earlier" = data **retention** period, **not** project duration. Do **not** change to four.
- **MEDIUM — DMSP alignment.** Retitle/align to current PAPPG **"Data Management and Sharing Plan (DMSP)"**
  terminology and confirm it addresses required elements (data types, formats, metadata/standards, access &
  sharing, re‑use, and archiving/retention). Add explicit **open‑source / open‑science** release commitment
  consistent with SaTC (code, benchmarks, attack/defense tools) — the proposal repeatedly promises these, so
  the DMSP should name them. Header currently reads "Data Management Plan."
- **LOW.** "workshop continuation proposal" appears only in a comment — no action.

### `sections/mentoring.tex` — Mentoring Plan — **HIGH + reframing advice**
- **HIGH — CAREER ref (L8).**
  - OLD: `…one undergraduate and one graduate student involved in this CAREER project.`
  - NEW: `…one undergraduate and one graduate student involved in this SaTC 2.0 RES project.`
- **LEAVE ALONE (L12, L20, L27, L32).** "career opportunities", "Career guidance", "career goals",
  "Career preparation" = job sense. **Do not change.**
- **Reframing advice (MEDIUM):** For RES, **de‑CAREER in place** — do **not** rebuild this as a TTE plan.
  Keep it as the mentoring content for the grad + undergrad researchers. **Verify requirement:** a formal
  **Mentoring Plan supplement is required only when the budget funds postdoctoral researchers** (PAPPG).
  This budget funds no postdoc, so the supplement may be **optional**; including it is harmless, but confirm
  against 25‑515/PAPPG whether it should be submitted as a separate supplementary doc vs. folded in.

### `sections/summary.tex` — Project Summary content (matches the real project) — **HIGH (one string)**
- **HIGH — CAREER ref (L26).**
  - OLD: `The educational components of this CAREER proposal integrate research findings…`
  - NEW: `The educational components of this project integrate research findings…`
- **NOTE / OK.** This file *correctly* describes the funded VLA‑security project and is the recommended
  **source content** to drop into `sections/0_project_summary.tex` (see that entry). No duration strings.

### `sections/synergy.tex` — Synergistic Activities
- **OK / CLEAN.** No CAREER/duration strings. No change.

### `sections/education.tex` — **not compiled** (commented out in `main_v2.tex`)
- **LOW / NOTE.** Contains lowercase "careers"/"career" (job sense, L3, L20) — **LEAVE ALONE.** No uppercase
  CAREER. If the plan is to reinstate an Education section for RES Broader Impacts, no de‑CAREER edits are
  needed here; just decide whether to `\input` it.

---

## 3. Budget conversion — what must change (no invented totals)

**Duration‑dependent (recompute for 4 years):** PI summer salary (4 summer months), grad‑student
stipend/tuition (4 yrs), undergrad hourly wages, fringe (L36), conference travel (L46, years 2–4),
Total Direct (L70), MTDC (L74 comment), Indirect @45.5% (L78), Total Direct+Indirect (L84).
**Duration‑independent (keep as‑is):** one‑time GPU workstation $12,500 (L61).
**Add:** SaTC **PI‑meeting travel** line (RES expectation).
**Constraints:** stays **single‑PI**; recomputed total should stay **< $600K** and far below the
**$1.2M RES cap (incl. optional TTE)** per NSF 25‑515. Exact dollar amounts are the **PI's recomputation** —
this report deliberately does not substitute new totals.

---

## 4. Other RES compliance items — status
- **Notion of trust:** already added in `01_v2.tex` (Overview defines trust). **OK.**
- **Responsible computing / responsible‑disclosure:** already added (`01_v2.tex` closing of Intellectual
  Merit gates offensive tooling). **OK** — ensure the same framing survives into the final Project Summary.
- **PI‑meeting travel:** **MISSING in budget** — add (see §2 budget). **HIGH.**
- **DMSP alignment:** **MEDIUM** — retitle/align and add explicit open‑source release commitment.
- **Keyword line in Project Summary:** **MISSING** — add (see §2, `0_project_summary.tex`), first token
  from the 25‑515 controlled list. **VERIFY the controlled vocabulary against the solicitation.**
- **Title consistency:** cover (`main_v2.tex`) OK; `0_project_summary.tex` must be updated to match. **HIGH.**

---

## 5. Strategic recommendations (alignment only)
- Make the **separate Project Summary the highest priority**: it currently advertises a different project;
  a topic mismatch between Summary and Description is a first‑impression reviewer red flag. Reuse
  `sections/summary.tex` content + add the keyword line.
- Keep the package **de‑CAREER‑ed rather than re‑scoped**: the science, mentoring, and education content map
  cleanly onto RES; no methodological redesign is needed — only identity, duration, budget, and keyword fixes.
- After edits, run one **global sweep** for `CAREER`, `five years`, `over five`, `2031`, `years 2 to 5`, and
  confirm only the intentional incidental uses remain (data retention in `datamanagement.tex`; experiment
  seed counts in `02_v2.tex`; lowercase job‑sense "career").
- **VERIFY against NSF 25‑515 primary text** (not assumed): exact RES duration cap, RES/TTE budget ceiling,
  the required Project‑Summary keyword vocabulary, and whether a Mentoring Plan supplement is required when
  no postdoc is funded.
