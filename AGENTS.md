# Skill maintenance

Follow [documentation-discipline](documentation-discipline/SKILL.md): README and
`docs/` are for human readers; `agents/` is for active agent context and progress.
Inspect affected human documentation when a task changes documented behavior,
interfaces, workflows, or design, and update it in place. Small fixes that preserve
the documented contract do not require a documentation review.

Keep these skills project independent. Put project-specific contracts in the
consuming repository, and keep skill instructions consistent with their discovery
descriptions. Validate edited skills with the skill-creator validator when available.

## Available skills

- [documentation-discipline](documentation-discipline/SKILL.md): human documentation and agent context maintenance.
- [paper-chart](paper-chart/SKILL.md): reproducible publication charts.

Installed skill directories link here from `~/.codex/skills/`.
