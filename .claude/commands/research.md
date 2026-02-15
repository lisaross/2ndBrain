# /research — Deep Research via NotebookLM

Research any topic using NotebookLM's deep research engine. Discovers sources, imports them into a notebook, and generates a briefing document.

**User input:** $ARGUMENTS

---

## Behavior

1. Create a dedicated research notebook:
   ```
   nlm notebook create "Research: $ARGUMENTS"
   ```
   Save the returned notebook ID.

2. Start deep research:
   ```
   nlm research start "$ARGUMENTS" -n <notebook-id> -m deep
   ```

3. Poll for completion (deep research takes ~5 minutes):
   ```
   nlm research status <notebook-id>
   ```
   Check every 30 seconds until status is complete.

4. Import discovered sources into the notebook:
   ```
   nlm research import -n <notebook-id>
   ```

5. Generate a briefing document:
   ```
   nlm report create <notebook-id> -f "Briefing Doc" -y
   ```

6. Wait for report generation:
   ```
   nlm studio status <notebook-id>
   ```

7. Download the report:
   ```
   nlm download report <notebook-id> -o ./research-<sanitized-topic>.md
   ```

8. Present the briefing document contents to the user with:
   - Key findings
   - Number of sources discovered and imported
   - Link to the notebook for further exploration

## Notes

- For quick results, the user can specify "fast" in their query to use `-m fast` mode (~30s, 10 sources).
- If `second-brain` exists, also create a note summarizing the research findings:
  ```
  nlm note create second-brain -c "<research summary>" -t "Research: $ARGUMENTS"
  ```
