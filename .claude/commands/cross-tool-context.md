# /cross-tool-context — Shared AI Context

Create a publicly shared NotebookLM notebook so any AI tool (Cursor, Copilot, ChatGPT, etc.) can access your project context.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Create the cross-tool context notebook:
   ```
   nlm notebook create "Cross-Tool Context — $(basename $(pwd))"
   ```

2. Register the alias:
   ```
   nlm alias set cross-tool-kb <notebook-id> -t notebook
   ```

3. Upload core project documentation as sources:
   ```
   nlm source add cross-tool-kb --file README.md -w
   nlm source add cross-tool-kb --file CLAUDE.md -w
   ```

4. If other documentation files exist (docs/, API specs, CONTRIBUTING.md, etc.), upload them:
   ```
   nlm source add cross-tool-kb --file <doc-file> -w
   ```

5. Pack the codebase structure (not full code, just structure) and upload:
   ```
   repomix . --output /tmp/cross-tool-structure.md --include "**/*.md"
   nlm source add cross-tool-kb --file /tmp/cross-tool-structure.md -w
   ```

6. Make the notebook public for sharing:
   ```
   nlm share public <notebook-id>
   ```

7. Get the sharing status/URL:
   ```
   nlm share status <notebook-id>
   ```

8. Create a summary note:
   ```
   nlm note create cross-tool-kb -c "<project summary, key patterns, conventions>" -t "Project Context Summary"
   ```

9. Update the Notebook Registry table in `CLAUDE.md` with the new notebook ID.

10. Report the public notebook URL and instructions for using it with other tools.

### If argument is `sync`

Sync updated documentation to the cross-tool KB:

1. List current sources:
   ```
   nlm source list cross-tool-kb
   ```

2. Re-upload changed documentation files:
   ```
   nlm source add cross-tool-kb --file README.md -w
   nlm source add cross-tool-kb --file CLAUDE.md -w
   ```

3. Check for and sync stale Drive sources:
   ```
   nlm source stale cross-tool-kb
   nlm source sync cross-tool-kb
   ```

4. Report what was synced.

### If no argument

Show the current state and sharing status:
```
nlm source list cross-tool-kb
nlm share status cross-tool-kb
```
