---
name: documentation-discipline
description: Keep repository documentation current and separate human-readable designs, behavior, and open design questions from agent progress and handoff context. Use when changing a repository, maintaining its docs, or scrubbing accumulated implementation diaries and stale status notes.
---

# Documentation discipline

Maintain documentation as an edited description of the project. Organize by subject and reader need; never treat human documentation as a chronological, append-only work log.

## Structure and adoption

- `README.md` and `docs/` serve human readers: orientation, current behavior, interfaces, usage, architecture, design rationale, and substantive open design problems. Component READMEs follow the same convention.
- `agents/` holds agent work context: active plans, progress, implementation diaries, handoffs, pending validation, operational state, and evidence pointers needed to resume work. Organize by ongoing goal; avoid one new file per session.
- Keep root `AGENTS.md` a concise instruction and navigation entry point. Put evolving handoff state under `agents/` and link to it.
- When adopting this convention in a repository, require a Markdown link in its `AGENTS.md` to this skill's actual `SKILL.md`, plus a short statement of the `docs/` / README versus `agents/` split and the obligation to inspect affected documentation on every change. Resolve the real installed or repository-local path; do not leave a placeholder or an unresolvable skill name. Prefer a repository-relative link if the skill is tracked there. Do not copy the entire skill into repository instructions.
- Link an `agents/` index from `AGENTS.md` when multiple active contexts need navigation. Create only directories and files with useful content. Human documentation must remain understandable without reading agent diaries.

This skill supplies maintenance rules, not permission for a wholesale repository rewrite. Apply routine maintenance to the current change; run the broader scrub workflow when requested. Creating this skill alone does not require scrubbing the current repository.

## Decide what belongs where

Write human documentation in terms of the system: what it does, why it works that way, how to use it, and what design choices remain unresolved. Describe an open design problem with its constraints, alternatives, tradeoffs, and decision criteria. Clearly identify proposals as proposals.

Keep session chronology, completed-task lists, next-agent instructions, pipeline IDs, transient reservations, paused experiments, and “X done; Y remains unverified” prose in `agents/`. Translate implementation activity into the resulting behavior when that behavior matters to readers. Do not merely move an entire mixed document: extract and integrate the durable explanation into the appropriate human topic.

Removing hedging must not turn an untested claim into a guarantee. State meaningful product constraints directly, such as “Automatic recovery is unsupported,” and keep test execution status in agent context. If behavior cannot be established, narrow or omit the claim and record the verification task under `agents/`. Preserve uncertainty that is itself part of a scientific result or unresolved design problem.

A reproducible evaluation, benchmark methodology, or design decision record can be useful human documentation. Preserve the assumptions, evidence, limitations, and reasoning readers need, while removing the surrounding execution diary. Keep datasets and reproduction scripts in their established supported locations; this convention does not relocate them or discard provenance.

## On every repository change

1. Inspect the README, documentation navigation, and human topic pages affected by the change. Follow relevant links and search for the changed behavior, interface, configuration, or design term. Do this even when the task did not explicitly request documentation edits. Keep inspection proportional to the affected scope.
2. Compare those descriptions with the changed source, interfaces, and accepted design intent. Reconcile contradictions and update the canonical explanation in place. Remove obsolete instructions and redundant status paragraphs; do not append a dated correction beneath stale text.
3. Update related examples and navigation where needed. If the existing docs remain accurate, leave them unchanged after inspection; do not add a “docs reviewed” entry to human documentation.
4. Refresh agent context only where continuation requires it. Record actionable remaining work, blockers, exact evidence references, and relevant validation results. Remove resolved tasks and replace obsolete state instead of accumulating contradictory handoffs.
5. Check the final diff for stale claims, broken local links, duplicated explanations, and progress prose leaking into human docs. Report actual validation in the task response or agent context, rather than adding a verification disclaimer to every human page.

## Scrub an existing repository

1. **Inventory and classify.** Read repository instructions and documentation entry points, then inspect topic pages and existing handoffs. Identify canonical human topics, mixed narrative, duplicate claims, obsolete material, and active agent state. Keep any migration checklist in `agents/` or temporary working output.
2. **Establish current meaning.** Reconcile conflicting text with relevant source and authoritative design decisions. Historical success does not establish current behavior. Preserve unresolved factual questions in active agent context; ask about unresolved intent only when it affects the rewrite.
3. **Extract human documentation.** Rewrite each canonical topic as a coherent account of current behavior, design, usage, or an open design problem. Consolidate overlapping pages. Retain substantive rationale and research qualifications. Replace chronological additions and progress summaries with integrated explanations.
4. **Extract active handoff state.** Under `agents/`, consolidate each ongoing goal into a compact account of the objective, current state, decisions and constraints, next actions, blockers, and evidence locations needed to continue. Preserve operational hazards such as frozen failure captures or restrictions on resets. Treat dated reservations and machine state as historical observations requiring recheck.
5. **Retire superseded text.** Remove resolved checklists, stale handoffs, duplicate narratives, and obsolete instructions from the active tree. Use Git history as the default historical record. If an old account has concrete reference value beyond Git history, summarize it and file it under `agents/archive/` with its historical scope and a pointer to the replacement. Preserve irreplaceable evidence before deletion, especially untracked material. Do not manufacture an archive of everything removed.
6. **Repair navigation and adopt the convention.** Update human indexes and inbound links to canonical topics; update agent navigation to active contexts. Add or correct the required `AGENTS.md` link to this skill and its concise directory convention. Remove dead links and links that present retired text as current guidance.
7. **Review the result as both readers.** A human should find the system explanation without reconstructing a campaign history. A successor agent should find the active objective, constraints, and next action without reading retired diaries. Check moved material for lost design rationale, unsupported guarantees, or discarded recovery context. Summarize what was consolidated or retired and any unresolved decisions in the task response.
