# Autonomous QA Loop Prompt

Use this pattern to create a neutral QA prompt for a fresh, independent,
history-free agent.

The review prompt must not disclose suspected bugs, intended fixes, prior
debugging conclusions, or areas you expect the reviewer to focus on. The goal
is to let each QA pass independently inspect the artifacts and surface issues
without inherited assumptions.

## Required Output Format

The generated QA prompt must contain exactly these four top-level sections, in
this order:

```text
Background
Goal (Original Request)
Review Target
Relevant Context Documents
```

Do not add sections such as `Known Issues`, `Expected Findings`, `Focus Areas`,
`Suggested Checks`, `My Diagnosis`, or similar leading guidance.

## Rules

- Keep the prompt neutral.
- Preserve the original user or business requirement in `Goal (Original Request)`.
- Do not rewrite the original requirement as the implementation's intended
  behavior unless that came from the original requirement.
- Put raw artifacts in `Review Target`: changed files, diffs, commits, output
  paths, test logs, generated reports, or commands that define what should be
  reviewed.
- Put authoritative context sources in `Relevant Context Documents`: docs,
  schemas, plans, interfaces, design notes, or files the reviewer may read.
- If old docs, old code paths, archived branches, or stale generated outputs
  are obsolete, state that fact in `Background`.
- If some scope must not be reopened, state it in `Background`.
- Include enough artifacts for review, but do not include expected issues.

## Template

```text
Background
<Current source-of-truth facts. State deprecated or out-of-scope docs/code.
State fixed boundaries that the reviewer must not reopen.>

Goal (Original Request)
<The original user requirement, as neutrally and faithfully as possible.>

Review Target
<Concrete artifacts to review: files, diffs, commits, outputs, commands, logs.>

Relevant Context Documents
<Authoritative docs and context files the reviewer may read.>
```

## QA Loop

1. Generate a neutral prompt with this pattern.
2. Run it in a fresh agent with no prior debugging conversation.
3. Fix only confirmed issues.
4. Start another fresh agent with a newly generated neutral prompt.
5. Repeat until independent passes stop finding meaningful defects.
