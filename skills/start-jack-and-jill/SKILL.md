---
name: start-jack-and-jill
description: Orient to a Jack & Jill organization, its recruiting assignments, notifications, protections, and the next safe action.
---

# Start with Jack & Jill

Use this skill when the user has just connected Jack & Jill or asks you to continue existing work.

Jack & Jill is a network of professionals who have chosen to be findable. You act for the connected organization. Every operation is attributed to its connection, and the organization can revoke access.

## Understand the workspace

- **Assignments** hold one hiring need and its shared, private, research, plan, and working context.
- **Pools** are temporary candidate sets. Search, filters, rankers, and pool algebra create new pools with traceable lineage.
- **Matches** are durable candidates committed from a pool. Feedback and communication attach to matches.
- **Reports** present matches to the principal and collect feedback.
- **Notifications** preserve task completions and feedback between sessions.
- **Protections** state the moderation rules for communication.

## Orient before acting

1. Call `whoami`. Confirm the connected organization and note recent assignments and notification state.
2. Call `list_notifications` from the last known sequence. Do not acknowledge notifications until you have processed them.
3. Call `list_protections` before drafting candidate communication.
4. Call `list_assignments` and identify the assignment relevant to the user's request.
5. For existing work, use `assignment_get`, `get_context`, `assignment_events`, `pools_list`, `tasks_list`, and `list_matches` to reconstruct its state.
6. Acknowledge processed notifications with `ack_notifications`.

If there is no assignment and no brief, explain that you can research a role, search the network, and build a shortlist, then ask what the organization needs.

Keep the assignment's `working` context current after meaningful progress. Write it for a competent colleague who has no conversation history.

Search and commit candidates only as the assignment requires. Outreach, introduction requests, and email need explicit user or principal direction. Silence is not authorization.
