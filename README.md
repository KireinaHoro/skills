# Shared skills

Project-independent Codex skills:

- [Documentation discipline](documentation-discipline/SKILL.md): maintain human documentation and separate agent work context.
- [Paper charts](paper-chart/SKILL.md): produce reproducible publication figures using each project's format and measurement contract.

Install by linking each skill directory into `${CODEX_HOME:-$HOME/.codex}/skills/`.
For example, from this checkout, when the destination does not already exist:

```sh
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s "$PWD/documentation-discipline" "${CODEX_HOME:-$HOME/.codex}/skills/documentation-discipline"
ln -s "$PWD/paper-chart" "${CODEX_HOME:-$HOME/.codex}/skills/paper-chart"
```

Keep project-specific paths, environments, acquisition rules, and publication
policies in the consuming repository's documentation and instructions.
