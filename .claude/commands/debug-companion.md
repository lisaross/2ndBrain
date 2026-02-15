# /debug-companion — Debugging Knowledge Base

Build and query a stack-specific debugging companion. Auto-detects your tech stack and loads debugging patterns, common errors, and solutions.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Detect the project's tech stack by examining:
   - `package.json` / `tsconfig.json` (TypeScript / Node.js)
   - `requirements.txt` / `pyproject.toml` / `Pipfile` (Python)
   - `*.sh` files, `Makefile`, `Dockerfile` (Shell / Bash)

2. Create the debug companion notebook:
   ```
   nlm notebook create "Debug Companion — $(basename $(pwd))"
   ```

3. Register the alias:
   ```
   nlm alias set debug-companion <notebook-id> -t notebook
   ```

4. Add stack-specific debugging resources as sources. For each detected technology, add relevant documentation URLs:
   ```
   nlm source add debug-companion --url <debugging-guide-url> -w
   ```

   Example URLs by stack:
   - **TypeScript / Node.js**: Node.js debugging guide, TS error reference, common error patterns
   - **Python**: Python debugging docs, common exceptions, traceback patterns
   - **Shell / Bash**: ShellCheck rules, common scripting pitfalls, exit code patterns

5. Add a note with the detected stack summary:
   ```
   nlm note create debug-companion -c "<detected stack and versions>" -t "Stack Profile"
   ```

6. Add a note with common error patterns for the detected stack:
   ```
   nlm note create debug-companion -c "<common errors and solutions>" -t "Common Error Patterns"
   ```

7. Update the Notebook Registry table in `CLAUDE.md` with the new notebook ID.

8. Report the detected stack and what was loaded.

### If argument is anything else

Treat the argument as a debug query:

1. Query the debug companion:
   ```
   nlm query notebook debug-companion "$ARGUMENTS"
   ```

2. Present the response with:
   - Suggested cause(s)
   - Recommended fix(es)
   - Related patterns from the knowledge base

3. If the debug companion has no useful answer, inform the user and offer to search the web instead.

### If no argument

Show the current state of the debug companion:
```
nlm source list debug-companion
nlm note list debug-companion
```
