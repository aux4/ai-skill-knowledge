# ai skill knowledge

Instruction-skill tests for the migrated `agent/skill-knowledge` package. These assume the
package is installed locally so the shared `ai:skill` profile and the
`aux4 ai skill validate`/`list` framework commands can discover it:

```bash
aux4 aux4 releaser install --dir packages/ai/ai-skill-knowledge/package --noBuild true
```

## prompt

### should output the knowledge base methodology heading

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
# Knowledge Base Skill
```

### should cover organizing entries

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
## Organize
```

### should cover standardizing entries

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
## Standardize
```

### should cover linking entries

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
## Link
```

### should cover searching entries

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
## Search
```

### should instruct the agent to run aux4 kb itself

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
aux4 kb
```

### should include the rules section

```execute
aux4 ai skill knowledge prompt
```

```expect:partial
## Rules
```

### should NOT reference the old copilot skills path

```execute
aux4 ai skill knowledge prompt | grep -c "copilot skills knowledge" || true
```

```expect
0
```

## native skill contract

### should be registered under the ai:skill profile

```execute
aux4 ai skill knowledge --help
```

```expect:partial
Methodology for running a kb knowledge base
```

### validate should pass

```execute
aux4 ai skill validate knowledge
```

```expect:partial
conforms to the native skill contract
```

### list should show knowledge

```execute
aux4 ai skill list
```

```expect:partial
knowledge
```

### should NOT expose a run command

```execute
aux4 ai skill knowledge --help | grep -c "  run" || true
```

```expect
0
```

### should NOT delegate to ai agent ask

```execute
grep -c "ai agent ask" ../.aux4 || true
```

```expect
0
```

### should NOT expose domain commands beyond prompt

```execute
aux4 ai skill knowledge --help | grep -cE "^  (add|search|update|ask|index|run) " || true
```

```expect
0
```
