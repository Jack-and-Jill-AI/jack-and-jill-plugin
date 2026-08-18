---
name: present-shortlist
description: Publish a concise Jack & Jill candidate report, collect principal feedback, and turn that feedback into the next search decision.
---

# Present a shortlist

Use this skill when committed matches are ready for the principal to review.

A report should make a decision easier. A list of names or scores in chat makes the principal reconstruct the work and gives you weak feedback.

## Build the report

1. Confirm candidates are durable matches with `list_matches`. Commit a reviewed pool first if needed.
2. Draft a title and `content_md` for `create_report`.
3. Use `CandidateCard` components with both `candidate_id` and `match_id`.
4. Group candidates with `CandidateGroup` when tiers or review modes help the decision.
5. Call `create_report` with `dry_run=true` and fix every finding.
6. Publish with `dry_run=false` and share the returned `view_url`.

The platform already renders the page title and date. Start `content_md` with the decision context, not a repeated heading.

Per candidate, add one or two sentences covering:

- the strongest profile-backed evidence for this assignment;
- the important caveat or unresolved question.

Do not repeat profile fields the card already displays. Do not state facts the profile does not support.

Use a grid for a small shortlist requiring deep comparison. Use review mode for a larger triage set. Put strong candidates who miss one stated preference in a separate tier and state the mismatch first.

Reports are immutable. Publish a successor when the shortlist changes, and use `archive_report` to disable the old report and its links.

## Use feedback

Review decisions arrive through notifications and match events. Read them with `list_notifications`, `match_get`, or `assignment_events`. Record feedback received elsewhere with `record_feedback`.

Look for the discrepancy between the principal's decisions and the plan. Ask one focused question about that discrepancy, then update `working`, `private`, `plan`, or the relevant filter or ranker.

A stalled search can still produce a useful report. Explain what was searched, what the pool statistics showed, and what decision or clarification is needed next.
