<p align="right">
  <a href="./README.md">English</a> · <strong>简体中文</strong>
</p>

# Codex Team Chat

`team-chat` 是面向 Codex Desktop 的公共 skill。它让当前 chat 负责目标、范围、授权和最终验收，让独立 chat 直接交换问题、证据和交接结果。

这个设计受 DeepSeek 的 [dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype) 启发，尤其借鉴了减少人的注意力成本、持续交付有用结果的工作方式。本项目是独立的 Codex skill，与 DeepSeek 或该项目没有隶属关系。

## 使用

调用 `$team-chat`，然后用自然语言描述任务：

```text
$team-chat 调查当前项目的费用统计，让一个 chat 调查，另一个 chat 交叉复核，最后由当前 chat 汇总。
```

Skill 会根据任务在当前 chat、原生子代理和独立 chat 之间选择。它遵守项目的授权、任务台账、工作目录和远端写入规则。只有当本任务授权覆盖参与者和通信范围时，独立 chat 才能互相发送消息。

## 安装

把仓库克隆到个人目录，再链接到 Codex 的个人 skill 目录：

```sh
mkdir -p ~/proj/codex-skills ~/.codex/skills
git clone https://github.com/Zn-Dk/codex-team-chat.git ~/proj/codex-skills/codex-team-chat
ln -s ~/proj/codex-skills/codex-team-chat ~/.codex/skills/team-chat
```

如果 `~/.codex/skills/team-chat` 已经存在，替换前先确认它不是仍在使用的本地副本。Codex 通常会自动发现 skill 更新；没有显示时重启 Codex。

## 实际验证

首轮 Codex Desktop 试点使用一个主控 chat、一个调查 chat 和一个复核 chat。三个 chat 完成了七条实质工作消息，其中四条消息在接收方上一轮结束后唤醒了空闲 chat；主控直接收到两份最终报告，没有手动转述工作 chat 的正常内容。

后续内部会话继续用它复用已有 chat，处理 worktree 协调、外部 readiness 检查和调查续接。实践证明，复用已有上下文、在授权或外部状态边界停下很有价值；复杂协调也会产生较多历史读取、有限等待和直接消息。发送成功并返回 thread ID 后，仍需从接收方核对真实 turn 和结果。

## 范围

这个 skill 定义本地多 chat 的角色、授权、交接消息、等待、恢复核对和验收方式。它不提供 GitHub 或 Lark 收件、持久队列、崩溃恢复或 exactly-once 投递；这些能力需要单独设计和验证。

需要独立 chat 时，阅读 [`references/protocol.md`](references/protocol.md)。

## 许可

MIT License，见 [`LICENSE`](LICENSE)。
