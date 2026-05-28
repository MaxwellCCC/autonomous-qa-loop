---
name: subtask-review-prompt
description: Create neutral independent-review, QA-loop, or subagent prompts for alpha-project code changes. Use when the user says QA循环, QA loop, QA cycle, 独立评审, 子任务评审, subagent review, reviewer prompt, QA agent, audit agent, or asks to draft prompts for reviewers to assess alpha changes without leading them toward known issues or expected findings.
---

# Subtask Review Prompt

Use this skill whenever Codex needs to draft a prompt for an independent
reviewer, QA-loop reviewer, or subagent to review alpha-side changes.

## Hard Format

The review prompt must contain exactly these four English top-level sections,
in this order:

```text
Background
Goal (Original Request)
Review Target
Relevant Context Documents
```

Do not add other top-level sections. Do not add sections such as `已知问题`,
`重点方向`, `预期发现`, `建议关注`, `我的判断`, or similar leading guidance.

## Neutrality Rules

- Keep the prompt neutral. Do not disclose suspected bugs, intended fixes,
  expected conclusions, or prior reviewer opinions.
- Describe the original user/business requirement in `Goal (Original Request)`; do not
  rewrite it as the implementation's intended behavior unless that came from the
  original requirement.
- Put raw artifacts in `Review Target`: changed files, diffs, commits, output paths,
  test logs, or commands that define what should be reviewed.
- Put context sources in `Relevant Context Documents`: authoritative docs, schemas, project
  plans, and files the reviewer may read.
- If some old documents, old code paths, archived branches, or stale generated
  outputs are obsolete, state that fact in `Background`.
- If some scope must not be reopened, state it in `Background`. Examples: do not
  revisit model-training policy, do not redesign portfolio logic, do not review
  deprecated V1/V2/V3 paths.

## Section Content

`Background` must explain the current facts the reviewer should accept before
starting:

- Current source of truth for facts, docs, data, and code.
- Which historical docs/code/output paths are deprecated or out of scope.
- Which scope boundaries are fixed and must not be re-litigated.
- Any environment constraints that matter for interpreting the review object.

`Goal (Original Request)` must preserve the user's original request:

- Quote or paraphrase the original requirement faithfully.
- Include acceptance criteria only when they came from the original request or
  an authoritative current doc.
- Do not include implementation diagnosis.

`Review Target` must identify the concrete artifacts to inspect:

- File paths, commit IDs, diff ranges, output directories, generated reports,
  or test commands.
- Prefer exact paths and raw evidence over summaries.
- Include enough artifacts for review, but do not include expected issues.

`Relevant Context Documents` must list documents the reviewer may use:

- Current authoritative context docs.
- Current schemas, enums, interfaces, or design notes needed to judge the change.
- Explicit notes when a listed document supersedes older material.

## Template

Use this exact skeleton and fill only what is known:

```text
Background
<Current source-of-truth facts. State deprecated/out-of-scope docs or code.
State fixed boundaries that the reviewer must not reopen.>

Goal (Original Request)
<The original user requirement, as neutrally and faithfully as possible.>

Review Target
<Concrete artifacts to review: files, diffs, commits, outputs, commands, logs.>

Relevant Context Documents
<Authoritative docs and context files the reviewer may read.>
```

## Final Check

Before sending the review prompt, verify:

- It has exactly four top-level sections.
- It does not mention known issues, suspected bugs, expected findings, or focus
  areas outside the four required sections.
- `Background` states source-of-truth, deprecated material, and non-reopenable scope.
- `Review Target` is artifact-based and reviewable without hidden conversation
  context.
