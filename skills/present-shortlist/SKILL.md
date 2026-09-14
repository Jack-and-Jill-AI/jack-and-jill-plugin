---
name: present-shortlist
description: Open the in-host Jack & Jill review app or publish a candidate report, then turn principal feedback into the next search decision.
---

# Present a shortlist

Use this skill when committed matches are ready for the principal to review.

A shortlist should make a decision easier. A list of names or scores in chat makes the principal reconstruct the work and gives you weak feedback.

## Review in the host when you can

Call `review_matches` with the `assignment_id` once the people are durable matches. This opens the candidate-review app in the connected host. Clicks write yes / maybe / no / intro through the app; you read those decisions later, you do not collect them with more tool calls.

- `view="review"` for one-at-a-time triage.
- `view="list"` for a small set that needs side-by-side comparison.
- Pass `match_ids` to choose the set. The app opens at most 50 matches.

Confirm the set with `list_matches` first. Commit a reviewed pool if the people are not matches yet.

## Publish a hosted report when a link is the point

Use `create_report` when someone needs a shareable page, or when the search stalled and you need a written progress note.

1. Draft a title and `content_md`.
2. Use `CandidateCard` components with both `candidate_id` and `match_id`.
3. Group candidates with `CandidateGroup` when tiers or review modes help the decision.
4. Call `create_report` with `dry_run=true` and fix every finding.
5. Publish with `dry_run=false` and share the returned `view_url`.

The platform already renders the page title and date. Start `content_md` with the decision context, not a repeated heading.

Per candidate, add one or two sentences covering:

- the strongest profile-backed evidence for this assignment;
- the important caveat or unresolved question.

Do not repeat profile fields the card already displays. Do not state facts the profile does not support.

Reports are immutable. Publish a successor when the shortlist changes, and use `archive_report` to disable the old report and its links.

## Use feedback

Review decisions arrive through notifications and match events. Read them with `list_notifications`, `match_get`, or `assignment_events`. Record feedback received elsewhere with `record_feedback`. An `intro` decision is recorded principal direction — it authorizes an introduction request.

Look for the discrepancy between the principal's decisions and the plan. Ask one focused question about that discrepancy, then update `working`, `private`, `plan`, a hard filter, or the relevant filter or ranker.

A stalled search can still produce a useful report. Explain what was searched, what the pool statistics showed, including `stats.hard_filters.description`, and what decision or clarification is needed next.
