# /stakeholder-brief — Stakeholder Communication

Distill complex technical or project work into executive summaries, presentation decks, audio overviews, and stakeholder-ready artifacts.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Create a stakeholder briefing notebook:
   ```
   nlm notebook create "Stakeholder Briefs — $(basename $(pwd))"
   ```
2. Register the alias:
   ```
   nlm alias set stakeholder-brief <notebook-id> -t notebook
   ```
3. Upload core project docs:
   ```
   nlm source add stakeholder-brief --file README.md -w
   ```
4. If a `second-brain` notebook exists, query it for recent progress and add as a note:
   ```
   nlm query notebook second-brain "Summarize all recent features, decisions, and progress"
   ```
   ```
   nlm note create stakeholder-brief -c "<progress summary>" -t "Project Progress"
   ```
5. Report completion.

### If argument is `update <context>`

Add new context for the next stakeholder update:
```
nlm note create stakeholder-brief -c "$ARGUMENTS" -t "Update: <date>"
```

### If argument is `exec-summary`

Generate an executive summary:
```
nlm report create stakeholder-brief -f "Create Your Own" --prompt "Create a concise executive summary suitable for senior stakeholders. Include: project status (on track/at risk/blocked), key accomplishments since last update, upcoming milestones, risks and mitigations, and decisions needed. Use clear, non-technical language. Keep it under 1 page." -y
nlm studio status stakeholder-brief
nlm download report stakeholder-brief -o ./exec-summary.md
```

### If argument is `slides`

Generate a presentation deck:
```
nlm slides create stakeholder-brief -y
nlm studio status stakeholder-brief
nlm download slide-deck stakeholder-brief -o ./stakeholder-deck.pdf
```

### If argument is `audio`

Generate a podcast-style audio briefing:
```
nlm audio create stakeholder-brief -y
nlm studio status stakeholder-brief
nlm download audio stakeholder-brief -o ./stakeholder-briefing.mp3
```

### If argument is `full`

Generate all stakeholder artifacts:

1. Executive summary (report)
2. Slide deck
3. Audio briefing

Run each in sequence, downloading all artifacts to `./stakeholder-artifacts/`.

### If argument is a question

Query the stakeholder context:
```
nlm query notebook stakeholder-brief "$ARGUMENTS"
```

### If no argument

Show notebook status:
```
nlm source list stakeholder-brief
nlm note list stakeholder-brief
```
