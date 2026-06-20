#### Description

The `prompt` command prints the knowledge-base methodology — the full guidance an agent reads on demand before curating, searching, or maintaining a kb knowledge base. It explains how to organize entries (folders by domain, one topic per entry, split vs merge), how to standardize each entry (consistent title, tags, content sections), how to link related entries (cross-reference by title, mark supersession), and how to search effectively (search before adding, specific-then-broad queries, search to locate then view to read).

This command reads `instructions/knowledge.md` from the package directory and writes it to stdout. Because `knowledge` is an **instruction skill**, this is its primary surface — there are no domain commands. The agent applies the methodology with its own `aux4 kb` calls (`add`, `search`, `view`, `list`, `update`, `remove`); the prompt does not run kb or call an LLM itself.

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

A knowledge base in `aux4/kb` is your durable, searchable memory ...
```
