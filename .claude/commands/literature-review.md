# /literature-review — Literature Review & Synthesis

Build a notebook from papers, articles, and URLs. Synthesize findings into briefing docs, mind maps, and structured summaries.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init <topic>`

1. Create a literature review notebook:
   ```
   nlm notebook create "Literature Review: <topic>"
   ```
2. Register the alias:
   ```
   nlm alias set lit-review <notebook-id> -t notebook
   ```
3. Run deep research to discover sources:
   ```
   nlm research start "<topic>" -n <notebook-id> -m deep
   ```
4. Poll for completion:
   ```
   nlm research status <notebook-id>
   ```
5. Import discovered sources:
   ```
   nlm research import -n <notebook-id>
   ```
6. Generate a briefing doc:
   ```
   nlm report create <notebook-id> -f "Briefing Doc" -y
   ```
7. Generate a mind map of themes:
   ```
   nlm mindmap create <notebook-id> -t "Literature Map: <topic>" -y
   ```
8. Report the number of sources found and key themes.

### If argument starts with `add`

Add sources to the literature review:

1. If URLs are provided:
   ```
   nlm source add lit-review --url <url> -w
   ```
2. If file paths are provided (PDFs, papers, notes):
   ```
   nlm source add lit-review --file <file-path> -w
   ```
3. If inline notes or annotations:
   ```
   nlm note create lit-review -c "$ARGUMENTS" -t "Note: <summary>"
   ```

### If argument is `synthesize`

Generate a synthesis of all sources:
```
nlm report create lit-review -f "Create Your Own" --prompt "Synthesize the key findings across all sources. Identify common themes, contradictions, gaps in the literature, and areas for further research. Organize by theme, not by source." -y
nlm studio status lit-review
nlm download report lit-review -o ./literature-synthesis.md
```

### If argument is `gaps`

Identify gaps in the research:
```
nlm query notebook lit-review "What are the gaps, contradictions, and unanswered questions across these sources? What areas need further research?"
```

### If argument is a question

Query the literature:
```
nlm query notebook lit-review "$ARGUMENTS"
```

### If no argument

Show the notebook status:
```
nlm source list lit-review
nlm note list lit-review
```
