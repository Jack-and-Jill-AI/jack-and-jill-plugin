---
name: run-assignment
description: Turn a hiring brief into a researched, planned Jack & Jill assignment and improve it through shortlist feedback.
---

# Run an assignment

Use this skill when a hiring brief arrives or an assignment needs a plan.

A brief records what the principal first thought to write down. The assignment must capture what they actually need. Close that gap before paying to search.

The working loop is:

**research → clarify → plan → search → present → feedback → revise**

## Start or recover the assignment

- For a new need, call `open_assignment` with a complete `shared_context` and any organization-confidential `private_context`.
- For existing work, read `assignment_get`, all relevant contexts with `get_context`, and recent `assignment_events`.
- Keep named assumptions and the next action in the `working` context with `revise_context`.

## Research before asking questions

Read the company, role source, recent company evidence, internal documents available to the user, and the backgrounds of relevant team members. Separate sourced facts from assumptions. Save a self-contained research note in the `research` context.

Ask only the questions that remain unanswered. For hiring, useful questions often include:

- compensation, location, remote policy, visa support, and seniority boundaries;
- the hiring timeline and how many candidates the principal can review each week;
- what outcome the hire must own and whose judgment defines a strong candidate.

Update `shared` with claims candidates may see. Keep confidential constraints and the real evaluation bar in `private`.

## Plan before searching

Write the `plan` context before calling `search_v2`. Include:

- one summary plus criteria per archetype (the default path);
- confirmed `hard_filters` (geography, years, languages, employers);
- optional exemplars, if the principal described real people;
- the base-path query, Filter, and Ranker only if v2's people were weaker;
- reference candidates, if the principal supplied them;
- expected funnel sizes, review cadence, and the daily-pass hour;
- what evidence would make the assignment pause for clarification.

Confirm the criteria with the user before the first search. Jack's network is large enough that a weak bar still returns a full pool of the wrong people, and a search takes about a minute. Skip a second confirmation for a trivial tweak they are already clearly in favour of.

A vague brief that cannot support a candidate-specific recommendation cannot support a commit. In that case, deliver the research and questions instead of running the funnel.

## Close the loop

Present committed matches with `review_matches`, or publish a report when a shareable link is the point. Read each feedback decision with `list_notifications`, `match_get`, or `assignment_events`. If feedback contradicts the plan, name the discrepancy, ask one sharp question, revise the relevant context or instrument, and search again.

The assignment is working when the principal is deciding between people rather than correcting your understanding of the role.
