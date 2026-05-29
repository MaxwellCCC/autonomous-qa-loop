# Autonomous QA Loop

English | [中文](#中文)

A portable prompt pattern for running fresh, neutral QA agents in repeated
loops. It works with coding agents that can review files, diffs, logs, test
output, or generated artifacts, and helps complex vibe-coded projects keep
surfacing new bugs instead of getting stuck in biased self-checks.

## Problem

AI coding agents are useful at self-review, but their later debugging passes
often become less effective. Once an agent has seen prior assumptions,
suspected fixes, or earlier conclusions, it tends to keep checking the same
areas and miss different classes of bugs.

For complex projects, the stronger pattern is to run repeated QA passes with
fresh agents that have no conversation history. Each pass should receive only
the original requirement, the concrete artifacts to inspect, and authoritative
context. The prompt must avoid leading the reviewer toward known suspicions or
expected findings.

## What This Provides

- A neutral review prompt structure for independent QA agents.
- A hard separation between original goal, review target, and context sources.
- Rules that prevent leaking suspected bugs, intended fixes, prior opinions, or
  expected conclusions.
- A repeatable QA-loop pattern: run a fresh agent, fix confirmed issues, then
  run another fresh neutral pass.
- A plain prompt file plus an optional packaged version for local agent tooling.

## Core Prompt

Use [PROMPT.md](PROMPT.md) with any agent. The generated QA prompt must contain
exactly four top-level sections:

```text
Background
Goal (Original Request)
Review Target
Relevant Context Documents
```

## Optional Codex Skill Install

Copy the included skill folder into your Codex skills directory:

```powershell
Copy-Item -Recurse .\autonomous-qa-loop $env:USERPROFILE\.codex\skills\
```

On macOS or Linux:

```bash
cp -R ./autonomous-qa-loop ~/.codex/skills/
```

Then start a new Codex session so the skill metadata is discovered.

Use it like this:

```text
Use $autonomous-qa-loop to draft a neutral prompt for a fresh independent QA agent.
```

## Repository Layout

```text
.
├── PROMPT.md
├── README.md
└── autonomous-qa-loop/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## License

CC0 1.0 Universal. You can copy, modify, redistribute, and use this prompt
pattern for any purpose.

## 中文

这是一个通用的“自动 QA 循环”提示词模式，用来让全新的、无历史上下文的独立
agent 反复审查复杂代码变更。任何能看文件、diff、日志、测试输出或生成物的
coding agent 都可以使用。

### 它解决的问题

vibe coding 做复杂项目时，经常会堆出很多隐藏 bug。让同一个 AI 自查虽然能发现
一部分问题，但第二、第三轮 debug 往往会被前面的上下文、猜测和修复方向影响，
很难继续发现新的问题。

更有效的做法是每一轮都开启一个全新的、无历史上下文的 agent，只给它原始需求、
具体审核对象和权威上下文，不告诉它已知怀疑、预期问题或前一轮结论。确认问题并
修复后，再开启下一轮新的中立审核。这样循环几轮，复杂项目里的 bug 会更容易被
系统性挖出来。

### 内容

- [PROMPT.md](PROMPT.md)：通用提示词规则，可给任何 agent 使用。
- `autonomous-qa-loop/`：可选的本地 agent 工具包装。

### Codex Skill 安装方式（可选）

```powershell
Copy-Item -Recurse .\autonomous-qa-loop $env:USERPROFILE\.codex\skills\
```

macOS 或 Linux：

```bash
cp -R ./autonomous-qa-loop ~/.codex/skills/
```

使用：

```text
Use $autonomous-qa-loop to draft a neutral prompt for a fresh independent QA agent.
```

### 许可证

CC0 1.0 Universal。你可以自由复制、修改、再发布，或用于任何目的。
