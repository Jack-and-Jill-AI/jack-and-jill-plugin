---
name: search-candidates
description: Search Jack & Jill with criteria and hard filters on the v2 path by default, then read profiles and commit a defensible shortlist.
---

# Search candidates

Use this skill once the assignment has useful `research` and `plan` contexts, and the user has confirmed the criteria (or the change is a trivial tweak they are already clearly in favour of). Jack's network is large enough that weak criteria still fill a 5,000-deep pool with the wrong people. A search takes about a minute, so confirm first rather than discovering that after the run.

Search creates temporary, immutable pools. Each operation branches a new pool so its lineage remains traceable. `commit` is the durability decision: it creates matches and copies pool provenance onto them. Nothing in search authorizes outreach.

Start on the v2 path. `search_v2`, `filter_v2`, and `rank_v2` share one criteria document, so the run is much faster than writing a query, sampling a Filter, and authoring a Ranker. Use `search`, `filter`, and `rank` when a sampled v2 pool is weaker than people you can find on the base path — and say so in `intent`.

## Plan for the limits

| Operation | Limit |
| --- | --- |
| `search` / `search_v2` | 5,000 candidates. Leave `search_v2` at the default. `top_n` is optional and is not 1,000. |
| `filter` / `rank` (base path only) | These two tools accept a pool of at most 1,000. That cap does not apply to `search_v2`, `filter_v2`, or `rank_v2`. |
| `filter_v2` | Top 2,000 of the pool it scored |
| `rank_v2` | Top 300 of a pool of 2,000 or fewer |
| Deep profile read | Pool of at most 250 |
| Sample page | 25 candidates |
| Commit | 100 candidates |

The default funnel is:

**`search_v2` (summary + criteria + confirmed hard filters) → sample → `filter_v2` → `rank_v2` → profile read → take → commit**

One set of criteria per archetype. Rank each, then `combine` the ranked pools. Do not union the searches and then score — a pool from two criteria sets has to be told which one. A useful shortlist is usually 5 to 15 people, not the maximum allowed.

## Run the v2 path

1. Call `search_v2` with `summary` and `criteria` (or `criteria_id`), plus the principal's confirmed `hard_filters`. Optional `exemplars` replace generated probes. Poll `task_get`.
2. Read `stats.hard_filters.description` and sample cards before spending on the next stage. Check `params.own_company_excluded`.
3. Call `filter_v2` on that pool. It finds the criteria through lineage — do not pass them again. Poll `task_get`. Members carry `criterion_scores`, `criteria_mean`, and `mismatches`.
4. Call `rank_v2` on the filtered pool. It returns per-criterion reasons, a `rationale`, `highlights`, and `p_intro` (the member `score`). Poll `task_get`.

Geography, years, languages, and employers belong in `hard_filters` on the search call, not in criteria. `filter_v2` and `rank_v2` do not take `hard_filters`; the search already enforced them.

## When the base path finds better people

If the sampled v2 pool is weaker than the need, switch:

1. Call `search` with a capabilities-and-outcomes `query`, useful `query_variants`, and the same `hard_filters`.
2. Create a Filter with `filter_create` (one evidence yes/no `criterion`), run `filter` with `sample_n=25`, read every reason, then run the full eligible pool.
3. Create a Ranker with `ranker_create`, call `rank`, and poll `task_get`.

The paths mix: a `search` pool can take `filter_v2` if you pass criteria; a `search_v2` pool can take your own Filter and Ranker.

## Read and commit

Use `sample` with `detail="profiles"` once the pool is within the deep-read limit. Read the candidates rather than relying on scores. Use `take` on the ranked pool, or `pool_create` for a hand-picked set, then call `commit` with the people you can defend to the principal.

Use a clear `intent` on writes, including which path you chose and why. Keep pool, task, and `criteria_id` values in the assignment's `working` context so another session can continue without repeating work.
