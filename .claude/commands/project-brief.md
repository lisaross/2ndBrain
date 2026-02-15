# /project-brief — Project Brief & PRD Hub

Create a notebook from PRDs, specs, and stakeholder documents. Generate summaries, study guides, and quick-reference briefings.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Create a project brief notebook:
   ```
   nlm notebook create "Project Brief — $(basename $(pwd))"
   ```
2. Register the alias:
   ```
   nlm alias set project-brief <notebook-id> -t notebook
   ```
3. Scan the project for documentation files and upload them:
   - README.md, CONTRIBUTING.md, CHANGELOG.md
   - docs/ directory contents
   - Any .md files in the project root
   ```
   nlm source add project-brief --file <doc-file> -w
   ```
4. Create a project overview note:
   ```
   nlm note create project-brief -c "<project name, goals, key stakeholders, timeline>" -t "Project Overview"
   ```
5. Generate a study guide for quick onboarding:
   ```
   nlm report create project-brief -f "Study Guide" -y
   ```
6. Update the Notebook Registry table in `CLAUDE.md` with the new notebook ID.
7. Report completion with source count.

### If argument starts with `add`

Add a new document to the project brief:

1. If the argument contains a file path:
   ```
   nlm source add project-brief --file <file-path> -w
   ```
2. If the argument contains a URL:
   ```
   nlm source add project-brief --url <url> -w
   ```
3. If it's inline text (PRD content, requirements, etc.):
   ```
   nlm source add project-brief --text "$ARGUMENTS" --title "<inferred title>" -w
   ```

### If argument is `brief`

Generate a briefing document from all sources:
```
nlm report create project-brief -f "Briefing Doc" -y
nlm studio status project-brief
nlm download report project-brief -o ./project-brief.md
```
Present the briefing to the user.

### If argument is `onboard`

Generate an onboarding study guide:
```
nlm report create project-brief -f "Study Guide" -y
nlm studio status project-brief
nlm download report project-brief -o ./onboarding-guide.md
```

### If argument is a question

Query the project brief:
```
nlm query notebook project-brief "$ARGUMENTS"
```

### If no argument

Show the notebook status:
```
nlm source list project-brief
nlm note list project-brief
```
