---
name: write-hiring-search
description: Write evidence-led search queries, must-have filters, and fit definitions for a Jack & Jill hiring assignment.
---

# Write hiring search inputs

Use this skill when drafting `search`, `filter_create`, or `ranker_create` inputs for a hire.

## Search for the person, not the job title

Describe capabilities, ownership, scale, and outcomes. For example:

> Hands-on research engineer who has trained or post-trained language models end to end, owns data, experiments, and production training infrastructure, and has shipped work beyond hosted API integration.

Add useful `query_variants` for adjacent language or backgrounds. Read score deciles, location statistics, and candidate samples as evidence about the market rather than forcing the results to match the brief.

## Filter only confirmed must-haves

Most searches need one or two evidence-based filters to reach the rank limit. A good criterion asks one answerable yes/no question:

> Has personally closed new-logo B2B SaaS deals in a quota-carrying role rather than only generating SDR or BDR pipeline?

Prefer demonstrated ownership over topic matching. "Has payments experience" is broad; "has personally built or operated payment or ledger systems" asks for evidence.

Do not use a filter only to shrink a pool. Location, attendance, work authorization, relocation, and current intent are often better handled as ranked preferences and verified during profile review.

Test each criterion with `filter` and `sample_n=25` before the full run.

## Rank overall fit and trade-offs

A ranker's `fit` is one clear paragraph covering:

- evidence of the work that matters;
- ownership and outcomes;
- weighted preferences and acceptable adjacent experience;
- facts that must not be inferred when absent.

Use references when the principal has named real examples. Scores order evidence; they do not decide whether someone should be hired or contacted.

Read full profiles before choosing. Commit the 5 to 15 people you can defend, even when they are not the literal top scores. Present a soft mismatch as a caveat rather than hiding it.
