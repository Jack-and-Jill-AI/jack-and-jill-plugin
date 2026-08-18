---
name: request-introduction
description: Request and complete a Jack & Jill candidate introduction after explicit principal direction and recorded candidate consent.
---

# Request an introduction

Use this skill only after the principal explicitly asks to meet a shortlisted candidate.

An introduction request reaches a real person's agent. Confirm authorization and ground every claim before sending it.

## Record principal direction

The match needs recorded introduction interest. This exists when the principal requested an introduction through a report or when their explicit direction was recorded with `record_feedback` and `decision="intro"`.

If neither happened, stop and ask. Silence is not permission.

## Write the request

Call `request_intro` with:

- the `match_id`;
- a short, candidate-specific `message`;
- an honest `intent`;
- a unique, stable `operation_key` for this intended request.

The message should:

- connect one concrete part of the candidate's work to the role;
- describe the opportunity only with claims in the assignment's `shared` context;
- say plainly that the principal would like an introduction;
- omit email addresses, phone numbers, and links.

If a useful claim is true but missing from `shared`, revise the shared context first. If it is not true for the assignment, leave it out.

A moderation block is a normal result. Read the findings, fix the unsupported or unsafe content, and retry with a new operation key only when the intended payload changed.

## Complete the double-opt-in introduction

Wait for candidate consent in `list_notifications` or `match_get`. Do not chase the candidate while consent is pending.

After both sides consent, call `send_intro_email` with the match ID, subject, Markdown body, intent, and a stable operation key. The principal and candidate receive the same moderated introduction email. This is the point at which contact details may cross the boundary.

Do not call `send_intro_email` before recorded candidate consent.
