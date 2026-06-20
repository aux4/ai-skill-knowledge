#### Description

The `knowledge` skill gives an agent a methodology for running a markdown knowledge base in `aux4/kb` — how to organize, standardize, link, and search entries so the kb stays high-signal and findable. It is contributed to the shared `ai:skill` profile (`aux4 ai skill knowledge ...`).

It is an **instruction skill**: it has no domain commands, no `run`, and no LLM dependency. It does **not** wrap `aux4 kb` — the agent already has `aux4 kb` (`add`, `search`, `view`, `list`, `update`, `remove`) and the LLM to reason. This skill supplies the *discipline* the agent applies with its own kb calls. Its only command is `prompt`, which prints the methodology on demand.

The methodology covers:

- **Organize** — folders by domain, one topic per entry, when to split vs merge.
- **Standardize** — consistent title, tags, and content sections so every entry has the same predictable shape.
- **Link** — cross-reference related entries by title and mark supersession explicitly.
- **Search** — search before adding (update over duplicate), query specific-then-broad, search to locate then view to read.

Load this skill when an agent is curating, searching, or maintaining a kb knowledge base. For trivial single lookups, the agent's direct `aux4 kb search` is enough — engage this skill when the quality and structure of the kb matters.

#### Usage

```bash
aux4 ai skill knowledge prompt
```

#### Example

```bash
aux4 ai skill knowledge prompt
```

```text
# Knowledge Base Skill
...
```
