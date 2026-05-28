# Subtask Review Prompt Skill

English | [中文](#中文)

A small Codex skill for drafting neutral independent-review, QA-loop, or
subagent-review prompts for code changes.

The skill is intentionally narrow: it helps an agent prepare a review prompt
that gives another reviewer enough context and artifacts to inspect, without
leaking suspected bugs, intended fixes, expected conclusions, or leading focus
areas.

## What It Enforces

- Exactly four top-level sections in the generated review prompt.
- The original user or business requirement is preserved separately from
  implementation details.
- Review targets are concrete artifacts such as files, diffs, commits, logs,
  generated outputs, or commands.
- Context documents are listed as references, not as conclusions.
- Known suspicions, expected findings, and prior opinions are excluded.

## Install

Copy the skill folder into your Codex skills directory:

```powershell
Copy-Item -Recurse .\subtask-review-prompt $env:USERPROFILE\.codex\skills\
```

On macOS or Linux:

```bash
cp -R ./subtask-review-prompt ~/.codex/skills/
```

Then start a new Codex session so the skill metadata is discovered.

## Usage

Ask Codex to use the skill when you need an independent reviewer prompt:

```text
Use $subtask-review-prompt to draft a QA loop review prompt for this change.
```

The generated prompt uses English section headings:

```text
Background
Goal (Original Request)
Review Target
Relevant Context Documents
```

## Repository Layout

```text
.
├── README.md
└── subtask-review-prompt/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## License

CC0 1.0 Universal. You can copy, modify, redistribute, and use this skill for
any purpose.

## 中文

这是一个很小的 Codex skill，用来生成中立的独立评审、QA 循环或子任务评审 prompt。

它的核心价值是把“原始需求”“审核对象”“相关上下文”分开，并禁止把已知怀疑、
预期结论或倾向性检查方向泄漏给评审者，从而降低评审 prompt 带偏的风险。

### 安装

把 skill 文件夹复制到 Codex skills 目录：

```powershell
Copy-Item -Recurse .\subtask-review-prompt $env:USERPROFILE\.codex\skills\
```

macOS 或 Linux：

```bash
cp -R ./subtask-review-prompt ~/.codex/skills/
```

然后开启新的 Codex 会话，让 Codex 重新发现 skill metadata。

### 使用

```text
Use $subtask-review-prompt to draft a QA loop review prompt for this change.
```

### 许可证

CC0 1.0 Universal。你可以自由复制、修改、再发布，或用于任何目的。
