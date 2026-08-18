---
name: resume-assignment
description: Recover a Jack & Jill assignment after a new session, task delay, handoff, or interruption without repeating paid work.
---

# Resume an assignment

Use this skill whenever you may not share context with the session that started the work.

Jack & Jill is the durable memory. Local notes and conversation history are only caches.

## Recover state

1. Call `list_notifications` from the last known sequence. Note completed tasks and new feedback.
2. Call `list_assignments` and identify the assignment.
3. Read `working`, `research`, `plan`, `shared`, and `private` with `get_context` as needed.
4. Read `assignment_events` after the last known sequence.
5. Call `tasks_list` with `status="inflight"` and the assignment ID.
6. Inspect relevant pools with `pools_list` and `pool_get`.
7. Read durable candidates with `list_matches` and, where useful, `match_get`.
8. Acknowledge only the notifications you have processed.

Filter and rank runs continue after disconnection. Poll an existing task with `task_get` before dispatching it again. Repeating a paid run can spend money without improving the result.

Pools may lose their members after expiry, but their descriptors preserve parameters, statistics, and lineage. Re-run the operation recorded by an expired descriptor rather than guessing what produced it. Matches and feedback remain durable.

After meaningful progress, update `working` with:

- the current phase;
- facts learned and assumptions still open;
- searches, instruments, pools, and tasks already tried;
- feedback received;
- the next safe action.

Done means a new session can state what happened and what comes next without relying on the previous conversation.
