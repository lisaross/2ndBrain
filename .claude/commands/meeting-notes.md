# /meeting-notes — Meeting Notes & Decisions

Capture meeting notes, decisions, and action items in a NotebookLM notebook. Query past meetings to recall decisions and context.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Create a meeting notes notebook:
   ```
   nlm notebook create "Meeting Notes — $(basename $(pwd))"
   ```
2. Save the returned notebook ID.
3. Register the alias:
   ```
   nlm alias set meeting-notes <notebook-id> -t notebook
   ```
4. Create an initial note with the notebook structure:
   ```
   nlm note create meeting-notes -c "This notebook captures meeting notes, decisions, and action items. Each meeting is added as a source or note with a date-stamped title." -t "About This Notebook"
   ```
5. Update the Notebook Registry table in `CLAUDE.md` with the new notebook ID.
6. Report completion.

### If argument starts with `add`

Capture a new meeting. Parse the remaining text for meeting details.

1. Create a note with the meeting content:
   ```
   nlm note create meeting-notes -c "$ARGUMENTS" -t "Meeting: <date> — <topic>"
   ```
   Structure the note with:
   - **Attendees** (if mentioned)
   - **Discussion Points**
   - **Decisions Made**
   - **Action Items** (with owners if mentioned)
   - **Open Questions**

2. Confirm what was captured.

### If argument starts with `import`

Import meeting notes from a file:
1. Upload the file as a source:
   ```
   nlm source add meeting-notes --file <file-path> -w
   ```
2. Confirm the import.

### If argument is a question

Query past meetings:
```
nlm query notebook meeting-notes "$ARGUMENTS"
```

Present the answer with references to specific meetings.

### If no argument

Show recent meetings and notebook status:
```
nlm note list meeting-notes
nlm source list meeting-notes
```
Summarize the number of meetings captured and date range.
