---
name: write-hiring-search
description: Write criteria, hard filters, and — only when needed — a query, must-have filter, and fit definition for a Jack & Jill hiring assignment.
---

# Write hiring search inputs

Use this skill when drafting the document a search will run. Default to one summary plus criteria for `search_v2`, `filter_v2`, and `rank_v2`. Those three stages read the same text, so you spend the time getting the bar right once. Write a `search` query, `filter_create` criterion, or `ranker_create` fit when a sampled v2 pool is weaker than people you can defend on the base path.

## Write one set of criteria

Criteria are the hiring bar. Every v2 stage reads exactly this text, so make each item a rock-solid, evidence-backed standard — not a topic and not a job title. Confirm the set with the user before the first search. Jack's network is large enough that weak criteria still return thousands of people, and the final pool follows that bar. A search takes about a minute, so a check now is cheaper than a wasted run. A trivial tweak the user is already clearly in favour of does not need another confirmation.

Pass `summary` (the work and the person) and three to twelve items, each a snake_case `key`, a short `title`, and a one- or two-sentence `summary` of what meeting it looks like. Or pass `criteria_id` to reuse a saved set. Identical content on the assignment is the same set.

```json
{
  "summary": "Founding account executive for a Series A developer-tools company selling to platform and infrastructure teams. Has built pipeline from nothing, closed six-figure new-logo deals with technical buyers, and can run discovery without an SE in the room.",
  "criteria": [
    {"key": "quota_attainment", "title": "Quota attainment", "summary": "Has carried and beaten a new-business quota in a closing role, with numbers they can name."},
    {"key": "technical_selling", "title": "Technical selling", "summary": "Sells to engineers and platform leads and can hold the technical conversation themselves."},
    {"key": "early_stage", "title": "Early stage", "summary": "Has been the first or second seller at a company and built the motion rather than inheriting one."},
    {"key": "outbound_motion", "title": "Outbound motion", "summary": "Generated most of their own pipeline through outbound rather than working inbound leads."}
  ]
}
```

Prefer demonstrated ownership over topic matching. "Has payments experience" is broad; "has personally built or operated payment or ledger systems" asks for evidence. Put a bar in the criterion summary when the difference matters ("shipped an LLM feature to production users, not a prototype").

Location, years, languages, and employers do not belong in criteria. Those are `hard_filters`.

One set of criteria per archetype you would hire. A sales role might get three — the ex-founder, the closer, the operator with the network — each its own v2 run. Optional `exemplars` (up to five profile-length sketches of the ideal person) replace generated probes so search looks for the people you describe.

## Put stated facts in `hard_filters`

`search` and `search_v2` take the same `hard_filters` object. They run inside the index before ranking, so the pool is already inside the constraint. Pass only sections the principal confirmed:

```json
{
  "hard_filters": {
    "geography": {"metros": ["LON"], "countries": ["GB"], "accept_relocate": true},
    "experience": {"min_years": 5},
    "languages": {"requirements": [{"language": "de"}], "match": "all"},
    "companies": {"exclude": {"current": [{"name": "Acme", "linkedin_path": "company/acme"}]}},
    "average_tenure": {"min_months": 18}
  }
}
```

| Section | Enforces | Not |
| --- | --- | --- |
| `geography` | metros (IATA), countries (ISO-2), regions, relocation, sponsorship, onsite days | commute radius |
| `experience` | completed dated years | seniority or level |
| `languages` | languages the profile states | English — it is refused |
| `companies` | exact employers by LinkedIn path | competitors by description |
| `average_tenure` | mean months per past role | current-role tenure |

Unknown facts are kept by default, so a filtered pool is "everyone not proven outside the constraint". An empty object or English-only spec is refused.

Your own company is added to `companies.exclude.current` on every search (`params.own_company_excluded`). People with under six months of dated tenure there can still appear. Put no-poach companies in `companies.exclude` from the first search.

The cheapest way to see a constraint's cost is to run the same search twice: once open, once with that constraint in `hard_filters`, and compare the counts. Read `stats.hard_filters.description` before you describe the pool.

## When the base path is the better tool

Use `search` / `filter` / `rank` when you have sampled the v2 pool and the people are weaker than the need — a query plus an authored must-have finds a set you can defend, and v2 did not. Say that in the write's `intent`.

A `search` query describes capabilities, ownership, scale, and outcomes, not a job title. `query_variants` broaden recall. A Filter `criterion` is one yes/no must-have; test it with `sample_n=25` before the full run. A Ranker `fit` is one paragraph of trade-offs, with references when the principal named real people. Scores order evidence; they do not hire.

Do not use a Filter to enforce location, attendance, visa, years, or employers. Those belong in `hard_filters`.
