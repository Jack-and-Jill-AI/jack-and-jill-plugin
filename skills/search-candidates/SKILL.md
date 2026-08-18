---
name: search-candidates
description: Search Jack & Jill, narrow candidate pools with tested filters, rank them, read profiles, and commit a defensible shortlist.
---

# Search candidates

Use this skill once the assignment has useful `research` and `plan` contexts.

Search creates temporary, immutable pools. Each operation branches a new pool so its lineage remains traceable. `commit` is the durability decision: it creates matches and copies pool provenance onto them. Nothing in search authorizes outreach.

## Plan for the limits

| Operation | Limit |
| --- | --- |
| Search | 5,000 candidates |
| Filter or rank input | 1,000 candidates |
| Deep profile read | Pool of at most 250 |
| Sample page | 25 candidates |
| Commit | 100 candidates |

The normal funnel is:

**search → tested must-have filter → rank → profile read → take → commit**

A useful shortlist is usually 5 to 15 people, not the maximum allowed.

## Search broadly enough to learn

Call `search` with capabilities and outcomes rather than only a title. Add `query_variants` when adjacent wording should broaden recall. Read the returned statistics and sample candidate cards before narrowing.

## Test a must-have before spending on the full pool

1. Create a saved filter with `filter_create`. For the simple path, supply one evidence-based yes/no `criterion`.
2. Call `filter` with `sample_n=25`.
3. Poll the returned task with `task_get`, respecting `next_poll_seconds`.
4. Read every sampled reason. Revise a criterion that passes the wrong people.
5. Run the validated filter over the full eligible pool.

Filter only requirements a profile can support with evidence. Treat location preference, attendance, work authorization, relocation, and current intent as facts to verify unless the profile states them clearly.

## Rank for overall fit

Create a named ranker with `ranker_create`. Its `fit` should explain the trade-offs and evidence that define a strong candidate. Add scored, reasoned references when the principal supplied real examples. Call `rank`, then poll `task_get` until the task returns the ordered pool.

## Read and commit

Use `sample` with `detail="profiles"` once the pool is within the deep-read limit. Read the candidates rather than relying on scores. Use `take` on the ranked pool, or `pool_create` for a hand-picked set, then call `commit` with the people you can defend to the principal.

Use a clear `intent` on writes. Keep pool and task IDs in the assignment's `working` context so another session can continue without repeating work.
