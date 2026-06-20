# agent/skill-knowledge

A native aux4 agent skill that gives an agent a **methodology** for running a markdown knowledge base in `aux4/kb` — how to organize, standardize, link, and search entries so the kb stays high-signal and findable.

It is an **instruction skill**: prompt-only, no domain commands, no `run`, and no LLM dependency. It does not wrap `aux4 kb`. The agent already has `aux4 kb` (`add`, `search`, `view`, `list`, `update`, `remove`) and the LLM to reason — this skill supplies the discipline the agent applies with its own kb calls. It depends on `aux4/ai-skill` only (for the shared `ai:skill` profile and the skill contract).

## Installation

```bash
aux4 aux4 pkger install agent/skill-knowledge
```

## Quick Start

```bash
aux4 ai skill knowledge prompt
```

This prints the methodology. The agent reads it, then manages the kb directly:

```bash
aux4 kb search "deploy tfstate" --folder .knowledge
aux4 kb add --folder .knowledge --topic "deploy: tfstate is local, no remote backend" --tags deploy,terraform --content "..."
```

## What the Methodology Covers

- **Organize** — folders by domain, one topic per entry, when to split vs merge so entries stand alone without duplicating.
- **Standardize** — every entry the same predictable shape: a specific searchable title, consistent reused tags, a one-line summary then supporting detail.
- **Link** — cross-reference related entries by exact title, mark supersession explicitly so two entries never silently disagree, use shared tags as soft links.
- **Search** — search before adding (update over duplicate), query specific-then-broad, search to locate then view only the top candidates.

Read the full guidance with `aux4 ai skill knowledge prompt`.

## Commands

This is an instruction skill — it contributes one command to the shared `ai:skill` profile.

| Command | Description |
|---------|-------------|
| `aux4 ai skill knowledge prompt` | Print the knowledge-base methodology (organize, standardize, link, search) |

## Native Skill Contract

This package conforms to the native aux4 skill contract:

- **scope `agent`, name `skill-knowledge`** — depends on `aux4/ai-skill` only; never on `aux4/kb`, `aux4/ai-agent`, or `aux4/copilot`. It is pure methodology; the agent that uses it already has kb.
- **`help.text` everywhere** — the required discovery layer (`aux4 ai skill knowledge --help`).
- **`man/ai_skill_knowledge__prompt.md` and `man/ai_skill__knowledge.md`** — the "is this a good fit?" tier.
- **`prompt`** — the methodology itself; this is an instruction skill so `prompt` is its primary surface.
- **No `run`, no domain commands** — running a skill is a runtime concern of `aux4/ai-agent`, and this skill teaches a method rather than performing a deterministic capability.

Verify conformance:

```bash
aux4 ai skill validate knowledge
aux4 ai skill list
```

## License

This package is licensed under the Apache-2.0 License.

See [LICENSE](./LICENSE) for details.
