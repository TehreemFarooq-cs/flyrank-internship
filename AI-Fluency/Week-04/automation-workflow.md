# Automation Workflow: Technical Article/Docs → Structured Study Notes

**Task automated (from Workflow Audit):** Task 2 - Summarizing long technical articles, documentation, or API guides

**Tool used:** NotebookLM (source-grounded research assistant)

---

## 1. Step Diagram

```
[1. GATHER]                [2. SYNTHESIZE]           [3. DRAFT]                  [4. REVIEW & FORMAT]
Add source (URL/PDF)  -->  NotebookLM extracts   -->  Structured notes       -->  Human checks accuracy
to NotebookLM notebook.    grounded content from      generated in fixed          against source, copies
Toggle off other           only the active            4-section format via        into Google Docs.
sources so this one        source (no outside         a single fixed prompt.
is isolated.                knowledge, no bleed
                            from other sources).
```

**Handoffs:**
- Gather → Synthesize: source must be fully processed (indexed) before querying, and all other sources toggled off to prevent cross-source bleed.
- Synthesize → Draft: same step in NotebookLM - the fixed prompt controls both extraction and formatting in one query.
- Draft → Review & Format: human reads the output, verifies it against the source, then manually copies it into Google Docs (no automated export).

---

## 2. Prompt / Configuration Used

**Tool setup:** One NotebookLM notebook ("Study Notes Pipeline"), 5 sources added individually. Before each run, all sources except the one being processed were toggled off in the source panel to keep each run grounded in a single source.

**The fixed prompt (used identically for all 5 runs):**

```
Using only the source I've added, generate structured study notes in this exact format:

## TL;DR
2-3 sentences on what this source covers and why it matters.

## Key Concepts
The core ideas explained simply, as bullet points.

## Code/API Specifics
Any function signatures, config options, parameters, or code patterns worth
remembering verbatim. Use code blocks. If none exist in the source, write
"None in this source."

## Gotchas / Open Questions
Anything confusing, version-specific, deprecated, or worth double-checking later.

Stay strictly grounded in the source — do not add outside knowledge or assumptions.
```

No other configuration, custom instructions, or tools were used - this is a single-prompt, single-tool pipeline by design, chosen because the "gather + synthesize + draft" work is naturally source-grounded and doesn't need a separate app/chaining tool like n8n.

---

## 3. Five Runs

| # | Source | Type | Time | Output Quality / Notes |
|---|--------|------|------|------------------------|
| 1 | React Compiler overview | Feature/blog-style explainer | ~2 min | Correctly pulled before/after code, flagged a real gotcha (inline arrow function memoization trap) not just surface-level summary. Accurate. |
| 2 | OpenAI API reference | API/technical reference docs | ~1 min | Correctly isolated from source 1 (no bleed). Pulled precise numeric details (header size limits, propagation delays) rather than vague paraphrase. Accurate. |
| 3 | HTML basics | Beginner/introductory tutorial | ~1 min | Appropriately scoped to beginner level rather than over-complicating simple material. Accurate. |
| 4 | iPhone battery-life tips | Non-technical listicle (edge case, not really "technical docs") | ~1 min | Correctly wrote "None in this source" for Code/API Specifics instead of inventing code to fill the template — did not hallucinate to fit the format. Accurate. |
| 5 | React Hooks reference | Dense API/reference docs | ~1-2 min | Richest code-example output of all 5 runs, matching the source's own code-heavy structure. Accurate. |

All 5 runs completed the format correctly with no cross-source contamination and no fabricated content. Generation time dropped after the first run (2 min → ~1 min) simply from familiarity with the tool's flow.

---

## 4. Time-Saved Estimate

**Manual baseline:** ~35 minutes to read one source and write equivalent structured notes by hand.

**Automated pipeline, per run (steady state, after setup):**
- Add source & wait for processing: ~1 min
- Run prompt & generation: ~1-2 min
- Human review against source + copy into Google Docs: ~2-3 min
- **~4-6 minutes per source**, roughly an **85-88% time reduction** per run vs. manual.

**One-time setup cost:** ~10 minutes (creating the NotebookLM account/notebook, writing and testing the prompt format across the first run or two).

**Totals across the 5 test runs:**
- Manual equivalent: 5 × 35 min = **175 minutes**
- Automated (setup + 5 runs): ~10 min setup + ~25 min total run time (including review/copy) = **~35 minutes**
- **Time saved: ~140 minutes (~2.3 hours) across 5 runs**, and the saving compounds further with every additional source since the setup cost is already paid.

---

## 5. Known Failure Points & Required Human Review

- **No automated export.** NotebookLM doesn't push output to Google Docs directly — every run ends with a manual copy-paste. This is the one step that can't be removed from human hands in this pipeline as built.
- **Cross-source bleed risk.** If sources aren't manually toggled off before a query, NotebookLM will draw from every active source in the notebook, silently breaking the "grounded in this source only" requirement. This gets riskier as more sources accumulate in one notebook over time — worth watching if this notebook keeps growing past 5 sources.
- **No relevance filtering.** The pipeline will happily generate well-formatted "study notes" even for a source that isn't really technical material (run #4, the battery-life listicle) — it doesn't flag "this doesn't really belong in a study-notes system," it just formats whatever it's given. A human has to decide upfront whether a source is worth running through the pipeline at all.
- **Accuracy still requires a human check.** Grounding and citation reduce hallucination risk substantially, but code/API details should still be spot-checked against the source before being trusted for real reference use — especially version-specific claims (e.g. exact propagation times, deprecated APIs).
- **Untested at scale.** All 5 runs used reasonably short/medium sources. Very long documents (full API references, long specs) weren't tested and may hit context or synthesis-quality limits not observed here.
