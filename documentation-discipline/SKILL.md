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

Keep session chronology, completed-task lists, next-agent instructions, pipeline IDs, transient reservations, paused experiments, and concrete validation tasks in `agents/`. Rewrite generic completion/verification hedging into specific state and next actions rather than relocating it verbatim. Translate implementation activity into the resulting behavior when that behavior matters to readers. Do not merely move an entire mixed document: extract and integrate the durable explanation into the appropriate human topic.

Removing hedging must not turn an untested claim into a guarantee. State meaningful product constraints directly, such as “Automatic recovery is unsupported,” and keep test execution status in agent context. If behavior cannot be established, narrow or omit the claim and record the verification task under `agents/`. Preserve uncertainty that is itself part of a scientific result or unresolved design problem.

A reproducible evaluation, benchmark methodology, or design decision record can be useful human documentation. Preserve the assumptions, evidence, limitations, and reasoning readers need, while removing the surrounding execution diary. Keep datasets and reproduction scripts in their established supported locations; this convention does not relocate them or discard provenance.

## Technical writing and epistemic precision

Apply these requirements to both human documentation and agent context.
Human documentation describes the current system authoritatively. Agent context
records concrete working state and continuation actions. Neither should read as
an audit of the agent's confidence; human documentation must not become a
research progress report.

- State established facts directly and concisely. Do not attach generic caveats,
  disclaimers, or verification-status qualifiers to paragraphs.
- Distinguish design intent, implemented behavior, and experimentally established
  behavior where the distinction matters. Describe proposals as proposals,
  source-supported behavior as implementation, and measured results within the
  actual experiment's scope. Never imply a test ran or a claim was proven without
  evidence; authoritative wording does not justify stronger claims.
- Express uncertainty only when it is specific, material, and actionable. Name
  the unresolved question, its consequence, and the decision or evidence needed
  to resolve it. Avoid boilerplate such as “remains unverified,” “not yet
  validated,” “further testing is needed,” or “subject to verification.”
- Collect genuine unresolved questions in a dedicated section instead of
  repeating them throughout a document. Keep substantive design questions in
  the relevant human topic; keep pending checks and operational blockers in
  agent context. Create no empty uncertainty section. Retain specific assumptions
  or experimental limitations beside claims when needed to interpret them.
- In agent context, state actual results and exact next checks with evidence
  pointers. For example, replace “Recovery remains unverified” with an actionable
  entry: “Open check: interrupt a write during restart and check that replay
  preserves acknowledged writes.” Do not imply that the proposed check has run.
- Rewrite outdated statements to describe the current system or working state.
  Do not append qualifications explaining their history; preserve historical
  rationale separately only when it still serves a concrete reader need.

## On every repository change

1. Inspect the README, documentation navigation, and human topic pages affected by the change. Follow relevant links and search for the changed behavior, interface, configuration, or design term. Do this even when the task did not explicitly request documentation edits. Keep inspection proportional to the affected scope.
2. Compare those descriptions with the changed source, interfaces, and accepted design intent. Reconcile contradictions and update the canonical explanation in place. Remove obsolete instructions and redundant status paragraphs; do not append a dated correction beneath stale text.
3. Update related examples and navigation where needed. If the existing docs remain accurate, leave them unchanged after inspection; do not add a “docs reviewed” entry to human documentation.
4. Refresh agent context only where continuation requires it. Record actionable remaining work, blockers, exact evidence references, and relevant validation results. Remove resolved tasks and replace obsolete state instead of accumulating contradictory handoffs.
5. Check the final diff for stale claims, broken local links, duplicated explanations, and progress prose leaking into human docs. Report actual validation in the task response or agent context, rather than adding a verification disclaimer to every human page.

## Scrub an existing repository

A scrub is an interactive, file-by-file review. Approval to start the scrub is
not approval to migrate every file. Stop for explicit user approval at the
per-file review below; silence or elapsed time is not approval. Do not batch
multiple source files into one approval or migrate later files in advance.

1. **Prepare the review queue.** Read repository instructions and documentation
   entry points, inspect Git status, and identify the documentation files in
   scope. Keep the queue in `agents/` or temporary output. Preserve unrelated
   edits. Inventorying files does not authorize rewriting them.
2. **Read one file and establish its meaning.** Inspect the complete document,
   relevant source, linked design decisions, and potential destination pages.
   Reconcile conflicting claims; historical success does not establish current
   behavior. Identify unresolved factual questions and intent that affects the
   proposed rewrite.
3. **Present the document and proposal, then STOP.** Identify and link the source
   file. Present its current contents for review; for a long document, provide a
   section-by-section account with relevant excerpts and a link to the complete
   text. Do not hide proposed deletions behind a vague summary. Before any
   migration edits, summarize what belongs in each category, explicitly marking
   empty categories:
   - **Human documentation:** current behavior, interfaces, usage, architecture,
     design rationale, substantive open design problems, and research methodology
     or qualifications. Name the destination paths and proposed restructuring.
   - **Active agent context:** objectives, decisions and constraints, next actions,
     blockers, pending validation, evidence pointers, and operational recovery
     state. Name the destination paths under `agents/`.
   - **Reference-only history:** material with concrete ongoing reference value;
     explain why a summary under `agents/archive/` is needed instead of Git history
     and identify its historical scope and replacement.
   - **Retire:** superseded, duplicate, or resolved text to remove, with reasons.
     Preserve irreplaceable evidence, especially untracked material.
   Include material remaining unchanged, unresolved questions, and all related
   destination/navigation files that the migration would modify. Ask the user to
   approve or revise this specific proposal and end the turn. Explain that this
   skill requires per-file approval and link to this workflow. Do not edit or
   commit the migration while approval is pending.
4. **Apply the approved migration.** Incorporate the user's corrections. Rewrite
   human explanations in place; preserve substantive rationale, research
   qualifications, and explicit proposal status. Consolidate active handoff state
   by goal, preserving hazards such as frozen captures and reset restrictions.
   Treat dated reservations and machine state as observations requiring recheck.
   Use Git history for retired material by default; do not archive everything.
   If new evidence materially changes the approved destinations, deletions, or
   meaning, present the revised proposal and stop for approval again.
5. **Validate and commit this file's migration.** Inspect the diff for lost
   meaning, unsupported guarantees, stale claims, and leaked progress prose.
   Repair inbound links and navigation affected by this migration and verify
   local links. Commit the source file together with its destination excerpts
   and necessary navigation updates as one coherent migration. Stage only the
   approved changes; never include unrelated edits. Do not defer commits until
   the end of the scrub or combine independently reviewed source files. If the
   approved action leaves the file unchanged, report that outcome without an
   empty commit. If validation or committing fails, resolve or report the issue
   before starting the next migration.
6. **Report and advance.** Report the commit and validation results, then present
   the next file using steps 2–3 and stop again. Keep active queue state compact;
   do not turn human documentation into a review diary. A destination receiving
   content from several source files receives incremental, separately approved
   migration commits. Push only according to the user's authorization and
   repository policy; per-file commits do not imply per-file pushes.
7. **Finish the scrub.** Check human and agent navigation across the migrated
   files. Ensure `AGENTS.md` links to this skill and states the directory
   convention; include any needed instruction changes in a per-file proposal
   before editing them. A human should understand the system without a campaign
   history; a successor agent should find active constraints and next actions
   without retired diaries. Present any additional corrective edits for approval
   through the same file-by-file loop. Summarize completed migrations and
   unresolved decisions in the final response.
