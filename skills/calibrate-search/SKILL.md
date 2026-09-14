---
name: calibrate-search
description: Improve Jack & Jill criteria, hard filters, and base-path instruments when samples, scores, or principal feedback disagree with the intended hiring bar.
---

# Calibrate search

Use this skill when a filter sample surprises you, a ranking contradicts your reading, or principal feedback exposes a gap in the plan.

Filters and rankers are named, revisable instruments. Pools retain the exact instrument revision that produced them, so improve the instrument rather than explaining away a weak result.

## Read filter samples honestly

Before a full filter run:

- read every sampled reason, including rejected candidates;
- distinguish a bad criterion from sampling noise;
- phrase criteria as demonstrated evidence, not broad topics;
- plan cap-sensitive decisions against uncertainty rather than one sample percentage.

A wrong threshold can be cheap to fix. A filter run caches its candidate outputs, so `refilter` can apply a new condition without another model run. A wrong extraction question needs a complete new filter shape through `filter_update`, or a new simple filter through `filter_create`.

Use `pack_schema` before writing a full filter query. A full filter separates:

- the facts to extract in `output_schema`;
- the pack fields supplied as `candidate_context`;
- the survival rule in `condition`.

## Anchor rankers with examples

A ranker's `fit` paragraph starts as a hypothesis. References make the scale concrete: candidate IDs with expected scores from 0 to 100 and evidence-backed reasons. Two or three useful examples often teach more than another paragraph of adjectives.

When observed ranking scores disagree with references, decide whether the fit definition is wrong or the reference no longer reflects the need. Use `ranker_update` with the complete revised name, fit, and reference set.

## Turn feedback into changes

Read feedback through `list_notifications`, `match_get`, and `assignment_events`. A rejection of someone who passed every instrument is evidence that the instruments may encode the original brief rather than the principal's need.

Trace the discrepancy to one place:

- a criterion's key, title, or summary (the default v2 instrument);
- a `hard_filters` section that should have been a preference, or a preference that belongs in `hard_filters`;
- on the base path, the search query, a Filter's evidence question, or the Ranker's fit.

Revise that element, explain why in the write's `intent`, update the assignment plan, and run the next pass. Calibration is complete when a feedback round no longer changes an instrument.
