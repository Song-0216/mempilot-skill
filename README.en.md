# MemPilot

A Chinese-first, Markdown-native, token-efficient project memory skill for coding agents.

**Status: `v0.1.0-alpha`**

MemPilot helps individual developers and small teams maintain long-running Vibe Coding projects. It creates human-readable project memory from the actual codebase, routes tasks to the most relevant module, reads only matching Markdown sections, and updates memory through minimal patches.

Key principles:

- Markdown is the source of truth
- no database or background service
- Top-1 module routing
- section-level reading
- incremental memory writes
- periodic health checks and cleanup
- Chinese project memory, original code identifiers preserved

The primary documentation is available in Chinese in [`README.md`](README.md).

## Quick start

Place the complete skill directory where your coding agent can discover skills, then say:

```text
帮我建记忆
```

See [`examples/vue-admin-demo`](examples/vue-admin-demo/README.md) for a generated project-memory example.

## Agent entry examples

Minimal entry examples for Codex, Claude Code, and Cursor are available in [`examples/agent-entries`](examples/agent-entries/README.md).

## Evaluation cases

Human-readable trigger, routing, and maintenance regression cases are available in [`evals/`](evals/).

## License

MIT
