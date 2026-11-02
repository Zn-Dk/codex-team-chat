# Codex Team Chat

`team-chat` 是一个面向 Codex Desktop 的公共 skill：由当前 chat 负责目标、范围和最终验收，让多个独立 chat 在同一任务内直接交换问题、证据和交接结果。

这个 skill 的设计受 DeepSeek 的 [dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype) 启发，尤其是“尽量减少人的注意力、持续交付有用结果”的工作方式。它是独立的 Codex skill，与 DeepSeek 或该项目没有隶属、赞助或代码合并关系。

## 使用

在 Codex Desktop 中调用 `$team-chat`，然后用自然语言描述任务：

```text
$team-chat 调查当前项目的费用统计问题，安排一个 chat 调查、另一个 chat 交叉复核，最后由当前 chat 汇总。
```

Skill 会根据任务选择主控、独立 chat 或原生子代理，并遵守当前项目的授权、台账、工作目录和远端写入规则。需要独立 chat 直接互相发送消息时，用户必须已授权本任务的参与者和通信范围。

## 安装

Codex 会从个人 skill 目录发现它。把仓库克隆到个人目录后建立软链接：

```sh
mkdir -p ~/proj/codex-skills ~/.codex/skills
git clone https://github.com/Zn-Dk/codex-team-chat.git ~/proj/codex-skills/codex-team-chat
ln -s ~/proj/codex-skills/codex-team-chat ~/.codex/skills/team-chat
```

如果 `~/.codex/skills/team-chat` 已存在，请先确认它不是仍在使用的本地副本，再替换成软链接。仓库内容更新后，Codex 通常会自动发现变更；没有显示时重启 Codex。

## 范围

这个 skill 规定本地多会话协作的角色、授权、消息交接、等待和验收方式。它不提供 GitHub、Lark、持久消息队列、跨重启恢复或 exactly-once 投递；这些能力需要另行设计和验收。

协议细节见 [`references/protocol.md`](references/protocol.md)。

## 许可

MIT License，见 [`LICENSE`](LICENSE)。
