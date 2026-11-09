# Independent Chat Protocol

Read this reference after deciding that independent chats are needed. Follow the live Codex Desktop tool schema when it differs from this document.

## Authorization and binding

- Use `list_projects` to locate the actual project, then use `create_thread` only within the user's authorization. Reuse an existing chat for the same task.
- Give every worker a self-contained role, file boundary, acceptance condition, controller route, peer routes, and workspace. Set the model and reasoning effort explicitly when the task requires it.
- If creation returns a `clientThreadId`, wait for setup and use the real `threadId` and `hostId` for later operations.
- Tell workers where the human authorization lives. Before a worker sends its first cross-chat message, it reads the controller thread to verify the original human confirmation and context. The manifest helps with routing; it does not create authorization.
- Authorization covers only the named participants and actions. A worker's request does not authorize a wider audience or a new external action.

Read-only work may share a checkout. For writes, assign ownership and serialize or isolate changes. Do not create a new worktree for every discussion turn.

## Delegation and direct messaging

Start the worker with the first actionable step. Let a passive reviewer wait for a concrete question or artifact instead of starting the same investigation.

Workers may call `send_message_to_thread` for authorized peers. A substantive message includes:

- the task or pilot ID;
- a unique message ID and `reply_to` value;
- the concrete question, handoff, or artifact path;
- the recipient's next step and stopping condition.

When a worker has sent a question and depends on the reply, record the checkpoint and end the worker's turn. Let the reply start the next turn. Do not keep the turn alive with a polling loop or make both workers wait for each other to finish. A reply that finds no correction should say why; do not manufacture a finding to complete a fixed number of rounds.

The controller owns scope and acceptance. Normal worker messages go directly between authorized participants. Route user scope changes through the controller. Do not send acknowledgements, thanks, or unchanged status updates that create a loop.

## Observe and recover

- Creation is asynchronous. Use one bounded `wait_threads` call for the current targets and carry forward each target's cursor.
- Use `read_thread` when checking a message, authorization, turn history, or artifact. A multi-target snapshot may represent different moments.
- A successful send that returns a thread ID proves only that the tool accepted the request. It does not prove that the receiver started, finished, or satisfied the acceptance condition. Check the receiver's message source, new turn, and artifact when that distinction matters.
- If a snapshot is stale, inspect the target's actual turn before retrying. Recover the failed layer—missing input, delivery, execution, or evidence—instead of repeating the whole handoff.
- Preserve the task's existing chats, authorization, message relationships, and artifacts when continuing. Check for duplicate message IDs before doing work twice.
- If the controller must relay content or re-dispatch a worker, record that intervention. A diagnostic run cannot call a manually relayed result direct autonomous communication.

## Delivery

Workers return the artifact, revision, validation result, and unresolved items to the controller, then end their turn. The controller verifies the substance and delivers one consolidated result. “Sent,” “the model said done,” and “review found nothing” each prove only their own layer.

This protocol does not provide a durable queue, exactly-once delivery, crash recovery, or external event intake. Test those properties separately. Keep ordinary collaboration evidence proportional to risk; log every send, receipt, idle state, and timestamp only when communication reliability itself is under test.
