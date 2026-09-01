# Durable Research Memory

[简体中文](README.zh-CN.md)

A lightweight `AGENTS.md` framework that keeps long-running research projects coherent across agent sessions.

Agent chat history is temporary. Project state should not be. This repository separates stable instructions, current execution state, research direction, and optional meeting communication so a new agent session can resume from verified evidence instead of a long context recap.

## The four layers

| Layer | File or system | Purpose |
| --- | --- | --- |
| Stable rules | `AGENTS.md` | Engineering constraints, memory protocol, and update discipline |
| Current state | `work_progress.md` and `work_progress/*.md` | Operational handoff, blockers, evidence, and exact next actions |
| Research direction | `RESEARCH_PROGRESS.md` | Hypotheses, durable conclusions, decisions, and roadmap |
| Communication | Optional Feishu meeting document | A concise, audience-facing research narrative |

The distinction matters: `work_progress.md` answers **what is happening now**; `RESEARCH_PROGRESS.md` answers **what the project currently believes and why**.

## Quick start

1. Copy [`AGENTS.md`](AGENTS.md) to the root of your research repository.
2. Optionally copy [`templates/work_progress.md`](templates/work_progress.md) to `work_progress.md`.
3. For an ongoing research project, optionally copy [`templates/RESEARCH_PROGRESS.md`](templates/RESEARCH_PROGRESS.md) to `RESEARCH_PROGRESS.md`.
4. Replace placeholders with facts verified from the repository. Leave unknowns explicitly unknown.
5. Start your coding agent from the repository root and ask it to continue the project.

Codex reads `AGENTS.md` before doing project work and supports layered instructions from the project root toward the current directory. See the [official OpenAI documentation](https://developers.openai.com/codex/guides/agents-md).

## Optional Feishu integration

The framework does not require Feishu. To let an agent read or update a Feishu group-meeting document, install and authenticate the official [Lark CLI](https://github.com/larksuite/cli) first:

```sh
npx @larksuite/cli@latest install
lark-cli config init --new
lark-cli auth login --recommend
lark-cli auth status
```

Some setup steps require browser authorization. Keep credentials out of the repository, grant only the permissions you need, and record the exact target document link in project-specific documentation.

## Design rules

- One concise root handoff, with topic files only when they earn their keep.
- Evidence before status claims.
- Updates at meaningful state transitions, not after every command.
- Stable knowledge moves to canonical documentation; stale progress is replaced, not accumulated.
- Research conclusions stay separate from run logs and implementation history.
- External meeting documents are presentation layers, never the source of truth.
- Repeated, stable workflows may graduate into project skills; one-off procedures do not.

## Compatibility

The file is designed for Codex and should also be useful with coding agents that recognize the [`AGENTS.md`](https://agents.md/) convention. Tool-specific behavior may differ, so verify instruction discovery in your agent before relying on it.

## License

[MIT](LICENSE)
