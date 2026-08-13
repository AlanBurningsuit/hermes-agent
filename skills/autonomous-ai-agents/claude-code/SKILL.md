---
name: claude-code
description: "Use when delegating bounded coding work to Claude Code."
version: 3.0.0
author: Hermes Agent + Teknium
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [Coding-Agent, Claude, Anthropic, Code-Review, Refactoring, Orchestration, Isolation]
    related_skills: [codex, hermes-agent, opencode]
---

# Claude Code Orchestration

## Scope Check

Loading this skill does not make Claude Code the right delegate. Use direct Hermes work, a Hermes subagent, another coding agent, or ordinary repository tools when the task is small, tightly coupled to the current conversation, not safely bounded, or does not benefit from a Claude-specific capability.

This skill is an orchestration discipline, not a CLI reference. It retains the stable decisions Hermes must make, maps the Claude-specific capability families that affect those decisions, and resolves current mechanics from live sources.

## Hermes Retains Ownership

Delegation does not transfer responsibility for the result. Hermes still owns:

- selecting and bounding the task;
- supplying decision-relevant repository instructions and context;
- choosing the working directory and required base state;
- defining file, command, Git, network, and outbound authority;
- preventing collisions with existing or concurrent work;
- reconciling concurrent writer outputs into the intended target state;
- specifying observable acceptance criteria;
- independently inspecting resulting files, Git state, and test output; and
- reporting verified outcomes rather than repeating Claude's account.

## Claude-Specific Capability Map

Use these capability families to decide what current interface to investigate. Names and command forms can change; verify them before launch.

- **Bounded non-interactive execution:** runs a prompt without an attached conversation UI, returns a final result, and exits. It suits a scoped task when the parent can wait and later interaction is unlikely. Current documentation describes this under programmatic or headless operation.
- **Native background sessions:** return control while a full Claude Code conversation continues without a terminal attached. They can expose supported status, later reply or attachment, and lifecycle operations. Investigate this family when work must outlive Hermes's foreground wait or may need later intervention; current anchors include background launch and agent view.
- **Attached interactive sessions:** keep a person or orchestrator continuously present in the full conversation. They suit exploration, frequent steering, or interfaces that require an attached terminal. Attachment is an interaction choice, not a prerequisite for every long task.
- **Continuation and resumption:** reopen saved conversational context or continue a prior run. Use this when accumulated reasoning is valuable; prefer a fresh run when reproducibility, changed instructions, or context separation matters more. Verify what state a resumed session restores and what launch configuration must be supplied again.
- **Isolated workspaces:** give concurrent writers separate file and branch state, commonly through worktrees or another currently supported isolation facility. Isolation prevents live edit collisions but does not coordinate related changes, decide which base state the worker needs, grant authority to commit or publish, or reconcile the result.
- **Machine-readable result or status surfaces:** non-interactive runs can expose structured results, while background-session management can expose scriptable state. Use supported structured surfaces when automation must distinguish completion, failure, or waiting-for-input; do not infer state by scraping an interactive UI when such a surface exists.

Absence from this map is not evidence that Claude Code lacks a capability. It means the capability did not earn permanent space here.

## Routing Questions

Characterise the task before choosing a familiar mode:

- Must Hermes wait for completion, or regain control while work continues?
- Is a final result sufficient, or may later interaction be needed?
- Must a person remain attached?
- Must work survive terminal detachment or support later resumption?
- Is machine-readable observation required?
- Could concurrent writers collide, including with an already dirty checkout?
- Which files, commands, Git operations, network access, and outbound acts are allowed?
- Is conversational continuity valuable, or is a reproducible fresh run preferable?
- Which exact repository state must Claude see: the current checkout, committed `HEAD`, an upstream base, or an isolated copy of in-progress work?

These are routing questions, not a fixed decision tree. Foreground, background, interactive, resumable, isolated, and externally orchestrated workflows are legitimate when their properties fit the task.

## Resolve Mechanics Live

Before constructing an invocation:

1. Resolve the installed executable and inspect its version.
2. Read the installed CLI's top-level help and the help for the relevant capability or subcommand.
3. If help does not establish lifecycle or workflow semantics, fetch Anthropic's machine-readable documentation index at https://code.claude.com/docs/llms.txt, select the relevant official page, and read its linked Markdown document.
4. Reconcile help and documentation with the installed version. If a remembered command or assumption disagrees with live help, discard the remembered form rather than forcing it.

Do not construct version-sensitive commands from memory. Do not treat omission from this skill or top-level help as proof that a capability is unavailable; the official index may expose a documented surface whose details are not shown there. Do not cache or reproduce the index, and do not add retrieval machinery around it.

## Delegation and Operation Loop

1. **Inspect state.** Read repository instructions and inspect branch, status, diff, concurrent work, and relevant tests. Completion: the intended base and collision risks are known.
2. **Bound the delegation.** State the outcome, in-scope paths, forbidden side effects, and acceptance criteria. Completion: Claude can tell what done means and what it may not do.
3. **Characterise operation.** Answer the lifecycle, interaction, observability, continuity, and isolation questions above. Completion: the required capability family is clear before any command is chosen.
4. **Resolve the interface.** Use live help and, where needed, the indexed official documentation. Completion: current syntax and lifecycle guarantees are supported by live sources.
5. **Launch in context.** Set the deliberate working directory and provide only decision-relevant context. Completion: the worker starts against the intended repository state with explicit authority.
6. **Monitor proportionately.** Use the supported result, status, logging, reply, or attachment surface appropriate to the chosen capability. Completion: Hermes can distinguish progress, input wait, completion, and failure without UI guesswork.
7. **Intervene on signal.** Step in for required input, approval, blockage, or material task drift—not merely because the work is slow.
8. **Reconcile and verify reality.** Inspect actual files and Git state. When writers ran concurrently, reconcile their outputs into the intended target state before running relevant checks independently. Completion: the combined state is coherent, and every claimed change and test result has parent-side evidence.
9. **Report.** State verified changes, commands and results, unresolved risks, and any work intentionally left undone.

For a dirty checkout, do not let delegation absorb unrelated work. A read-only task may run against it if that state is intentionally part of the evidence. A writer needs either non-overlapping, explicitly protected scope or isolation based on the correct starting state; verify current isolation/base semantics before assuming a new workspace contains local uncommitted changes.

## Durable Failure Modes

- Choosing a familiar mode before characterising the task.
- Constructing commands from remembered syntax.
- Delegating without a bounded outcome or acceptance criteria.
- Allowing side-effect authority to emerge implicitly from tool access.
- Running overlapping writers without deliberate coordination, and without isolation where needed.
- Treating an isolated workspace as authority to commit, push, publish, merge, or deploy.
- Scraping an interactive UI when a supported result or status surface exists.
- Killing slow work without checking whether it is progressing or waiting for input.
- Accepting Claude's report as proof of changed files or passing tests.
- Adding newly discovered flags, schemas, UI details, or version inventories to this skill instead of leaving current mechanics with their owning source.

## Verification Checklist

- [ ] The task benefits from Claude Code rather than delegation by habit.
- [ ] Repository instructions, current state, and intended base were inspected.
- [ ] Outcome, scope, authority, and acceptance criteria were explicit.
- [ ] Lifecycle, interaction, observability, continuity, and isolation needs were characterised.
- [ ] Current invocation syntax and non-obvious lifecycle semantics were resolved live.
- [ ] Concurrent or pre-existing work cannot be overwritten or silently absorbed.
- [ ] Monitoring uses a supported interface appropriate to the workflow.
- [ ] Actual files, Git state, and relevant tests were checked independently.
- [ ] The report separates verified outcomes from Claude's unverified claims.
