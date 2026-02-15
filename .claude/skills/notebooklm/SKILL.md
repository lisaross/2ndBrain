# NotebookLM Skill

This skill auto-triggers when Claude Code interacts with NotebookLM via the `nlm` CLI. It provides context about available notebooks, CLI commands, and workflow patterns.

## Activation Triggers

This skill activates automatically when:

- The user mentions NotebookLM, NLM, or notebook operations
- A debugging session starts (to query debug-companion first)
- A feature is marked complete (to update second-brain and check security)
- Documentation files are modified (to sync cross-tool-kb)
- The user invokes any of the 7 slash commands

## Available Notebooks

Check `CLAUDE.md` for the current Notebook Registry. The four standard notebooks are:

1. **second-brain** — Project knowledge base for features, decisions, context
2. **debug-companion** — Stack-specific debugging patterns and solutions
3. **security-handbook** — OWASP top 10 and security best practices
4. **cross-tool-kb** — Shared context across AI tools

## Automatic Behaviors

### After Feature Completion
When a feature is completed and the build passes:
```
nlm note create second-brain -c "<what was built, key decisions, files changed>" -t "Feature: <name>"
```

### When Debugging
Before searching the web for error solutions:
```
nlm query notebook debug-companion "<error message or description>"
```
Only proceed to web search if the debug companion has no relevant answer.

### Before Marking Feature Complete
Query the security handbook for relevant risks:
```
nlm query notebook security-handbook "security risks for <feature description>"
```

### When Docs Change
When README.md, CLAUDE.md, docs/, or API specs are modified:
```
nlm source add cross-tool-kb --file <changed-file> -w
```

## CLI Reference

See `references/nlm-cli-reference.md` for the complete NLM CLI command reference.

## Error Handling

- If an `nlm` command fails with an auth error, prompt the user to run `nlm login`.
- If an alias is not found, check `nlm alias list` and suggest running the relevant `/init` command.
- If a notebook ID is invalid, run `nlm notebook list` to find valid IDs.
- If source upload fails, check file size (NotebookLM has limits) and suggest splitting large files.
