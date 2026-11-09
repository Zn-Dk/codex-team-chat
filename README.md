<p align="right">
  <strong>English</strong> · <a href="./README.zh.md">简体中文</a>
</p>

# Codex Team Chat

`team-chat` is a public skill for Codex Desktop. It turns the current chat into a controller that owns the goal, scope, authorization, and final acceptance while independent chats exchange questions, evidence, and handoffs directly.

The design is inspired by DeepSeek's [dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype), especially its focus on reducing human attention cost while delivering useful results. This is an independent Codex skill and has no affiliation with DeepSeek or that project.

## Use it

Invoke `$team-chat` and describe the work in natural language:

```text
$team-chat Investigate the current project's cost reporting and have one chat cross-check the result before you summarize it.
```

The skill chooses between the current chat, native subagents, and independent chats based on the task. It follows the project's authorization, task ledger, workspace, and remote-write rules. Independent chats may message one another only when the task authorization covers those participants and that communication.

## Install

Clone the repository and link it into your personal Codex skills directory:

```sh
mkdir -p ~/proj/codex-skills ~/.codex/skills
git clone https://github.com/Zn-Dk/codex-team-chat.git ~/proj/codex-skills/codex-team-chat
ln -s ~/proj/codex-skills/codex-team-chat ~/.codex/skills/team-chat
```

If `~/.codex/skills/team-chat` already exists, check whether it is an active local copy before replacing it with the symlink. Codex normally discovers changes automatically; restart Codex if the updated skill does not appear.

## Observed validation

An initial Codex Desktop pilot used one controller plus independent investigator and reviewer chats. The chats exchanged seven substantive work messages, four messages woke a chat after its previous turn had ended, and the controller received both final reports without relaying normal worker messages by hand.

Later internal sessions reused existing chats for worktree coordination, external-readiness checks, and follow-up investigations. They showed the value of reusing a task's existing context and stopping at authorization or external-state boundaries. They also showed the cost: complex coordination can require many history reads, bounded waits, and direct messages. A successful send that returns a thread ID still needs receiver-side verification.

## Scope

This skill defines local multi-chat roles, authorization, handoff messages, waiting, recovery checks, and acceptance. It does not provide GitHub or Lark intake, a durable queue, crash recovery, or exactly-once delivery. Those capabilities need separate design and validation.

Read [`references/protocol.md`](references/protocol.md) when independent chats are needed.

## License

MIT License. See [`LICENSE`](LICENSE).
