# /explain-codebase — Codebase Visualization

Pack a codebase with repomix, upload to NotebookLM, and generate architecture visualizations (mind maps, infographics).

**User input:** $ARGUMENTS

---

## Behavior

### Determine the target

- If argument is `.` or empty: use the current working directory
- If argument is a local path: use that directory
- If argument is a GitHub URL: clone to a temp directory first
  ```
  git clone <url> /tmp/explain-codebase-repo
  ```
  Then use `/tmp/explain-codebase-repo` as the target.

### Steps

1. Pack the codebase with repomix:
   ```
   repomix <target-dir> --output /tmp/codebase-explain.md
   ```
   For large codebases, focus on source code:
   ```
   repomix <target-dir> --output /tmp/codebase-explain.md --ignore "node_modules,dist,build,.git,vendor"
   ```

2. Create a notebook for this codebase:
   ```
   nlm notebook create "Codebase: $(basename <target-dir>)"
   ```

3. Upload the packed codebase:
   ```
   nlm source add <notebook-id> --file /tmp/codebase-explain.md -w
   ```

4. If a README exists in the target, upload it too:
   ```
   nlm source add <notebook-id> --file <target-dir>/README.md -w
   ```

5. Generate a mind map of the architecture:
   ```
   nlm mindmap create <notebook-id> -t "Architecture: $(basename <target-dir>)" -y
   ```

6. Generate an infographic:
   ```
   nlm infographic create <notebook-id> -y
   ```

7. Wait for artifacts:
   ```
   nlm studio status <notebook-id>
   ```

8. Download artifacts:
   ```
   nlm download mind-map <notebook-id> -o ./codebase-mindmap.json
   nlm download infographic <notebook-id> -o ./codebase-infographic.png
   ```

9. Query the notebook for a high-level architecture summary:
   ```
   nlm query notebook <notebook-id> "Describe the high-level architecture, main components, and how they interact"
   ```

10. Present results to the user:
    - Architecture summary from the query
    - Mind map file location
    - Infographic file location
    - Notebook ID for further exploration
