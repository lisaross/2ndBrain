# /second-brain — Project Knowledge Base

Manage the project knowledge base notebook. This notebook captures features, architectural decisions, and project context as a living document.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Create a new notebook:
   ```
   nlm notebook create "Second Brain — $(basename $(pwd))"
   ```
2. Save the returned notebook ID.
3. Register the alias:
   ```
   nlm alias set second-brain <notebook-id> -t notebook
   ```
4. Pack the current codebase with repomix and upload as a source:
   ```
   repomix . --output /tmp/codebase-pack.md
   nlm source add second-brain --file /tmp/codebase-pack.md -w
   ```
5. Upload the README as a source:
   ```
   nlm source add second-brain --file README.md -w
   ```
6. Upload CLAUDE.md as a source:
   ```
   nlm source add second-brain --file CLAUDE.md -w
   ```
7. Create an initial note summarizing the project:
   ```
   nlm note create second-brain -c "<project summary based on README and codebase>" -t "Project Overview"
   ```
8. Update the Notebook Registry table in `CLAUDE.md` with the new notebook ID.
9. Report completion with the notebook ID and source count.

### If argument is anything else

Treat the argument as context to add to the knowledge base:

1. Create a note capturing the provided context:
   ```
   nlm note create second-brain -c "$ARGUMENTS" -t "Update: <short summary>"
   ```
2. If the argument references specific files, also add them as sources:
   ```
   nlm source add second-brain --file <referenced-file> -w
   ```
3. Confirm what was added.

### If no argument

Query the current state of the knowledge base:
```
nlm source list second-brain
nlm note list second-brain
```
Report a summary of sources and notes in the notebook.
