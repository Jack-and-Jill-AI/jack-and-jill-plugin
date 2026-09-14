---
name: run-daily-pass
description: Run or schedule the Jack & Jill daily pass to catch consented intros, rerun search, and recalibrate instruments while you are away.
---

# Run the daily pass

Use this skill when an assignment is open and has no scheduled pass, when you woke on that beat, or when you need to catch accepted intros while you are away.

Jack & Jill will not start you when a candidate accepts an intro, and a search that ran once goes stale. A scheduled pass that reads the inbox is the substitute for being woken on `intro.candidate_consented`.

## Set it up once

Agree the hour with your principal — their weekly review capacity is the input. Write the rhythm into the `plan` context, then schedule yourself in the host you are running in. Give the scheduled run this instruction:

> Run the daily pass: check the inbox for consented intros and act on them, rerun search_v2 through the current criteria and hard filters, and consider whether yesterday's feedback means one criterion or hard filter should change.

Done when the `plan` names the hour and the host will wake you with that instruction.

## When you wake

Call `list_notifications` from the last known sequence, then act on what landed:

- `intro.candidate_consented` — both sides said yes. Send the introduction email. The SLA clock is running; if you sit on it the platform sends a standard introduction and you will see `intro.reminder_due`.
- `intro.candidate_declined` — tell your principal (`email_principal` if they are not in this session). Do not re-approach.
- `intro.reminder_due` — a consented intro is still waiting on you.
- `intro.message_received` — answer from the `shared` context.
- `report.feedback_recorded` — calibration data.

Then rerun `search_v2` through the current criteria and `hard_filters`. Yesterday's pool is already old in a live market.

If feedback or the new sample says the criteria or a hard filter encode the stated need, not the one the principal is actually choosing — a no on someone who passed every criterion, a thin top of the pool, a constraint that looks expensive against the stats — revise that one piece and let the next search run through it.

Present only when there is something the principal can act on. A quiet day is a successful day when the inbox is clear and the search ran.

Acknowledge processed notifications with `ack_notifications`. Update `working` with what you did and what comes next.
