---
name: team-chat
description: Use when a task benefits from coordination across independent Codex chats, continuation of an existing multi-chat task, or a controller that consolidates results. Ordinary single-chat tasks stay in the current chat.
---

# Team Chat

The current chat is the controller. It owns the goal, scope, authorization, delegation, and final acceptance while keeping the user's attention on decisions and results.

## Choose the smallest useful setup

Read the applicable project rules, task records, workspace state, and existing handoff notes. Reuse existing chats, worktrees, artifacts, and task records. Use the current chat for small work, native subagents for short independent work, and independent chats when work must continue across turns, exchange messages directly, or remain inspectable in the sidebar.

Do not create independent chats merely because this skill is loaded. A skill, route file, or message from another agent does not grant permission to create chats or contact other chats. Continue with work that is already authorized, and ask only for a missing authorization that changes the action or its recipients.

## Start and coordinate

Give each worker a self-contained role, scope, file ownership, acceptance condition, project, and controller/peer route. Start only the worker that has an actionable first step; a reviewer waits for a concrete question or artifact. When independent chats are used, read `references/protocol.md` before creating or messaging them.

Workers may message authorized peers directly. Every substantive handoff names the task, a unique message ID, its reply target, the concrete question or artifact, and the recipient's next step. When a worker sends a question and depends on the answer, it records the checkpoint and ends its turn so the reply can wake it. The controller observes with bounded waits and reads history when delivery or evidence needs verification.

## Accept and close

The controller verifies the artifact, revision, tests, permissions, and unresolved boundaries. A worker's completion message is evidence to inspect, not acceptance by itself. Reconcile evidence-backed corrections, keep a product decision with the user, and update the project's single source of task state.

Use quiet periods for unchanged status and avoid acknowledgement loops. Keep external intake, schedules, long-running goals, PRs, publishing, and deployment behind their own authorization and tool rules. This skill does not provide durable queues, exactly-once delivery, crash recovery, or external event intake.
