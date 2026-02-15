# /knowledge-base — General-Purpose Knowledge Base

Create a general-purpose NotebookLM notebook for any domain — onboarding docs, process guides, FAQs, team knowledge, or personal learning.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init <name>`

1. Create a knowledge base notebook:
   ```
   nlm notebook create "KB: <name>"
   ```
2. Register the alias using a sanitized name:
   ```
   nlm alias set kb-<sanitized-name> <notebook-id> -t notebook
   ```
3. Create a welcome note:
   ```
   nlm note create kb-<alias> -c "Knowledge base: <name>\nCreated: <date>\n\nThis notebook is a general-purpose knowledge base. Add sources (files, URLs, text) and query them with natural language." -t "About This KB"
   ```
4. Report the alias and notebook ID.

### If argument starts with `add`

Add knowledge to the KB. Determine the alias from context (most recent or specified).

1. If URLs:
   ```
   nlm source add <kb-alias> --url <url> -w
   ```
2. If files:
   ```
   nlm source add <kb-alias> --file <file-path> -w
   ```
3. If inline knowledge (processes, FAQs, how-tos):
   ```
   nlm source add <kb-alias> --text "$ARGUMENTS" --title "<topic>" -w
   ```

### If argument is `faq`

Generate an FAQ from the knowledge base:
```
nlm report create <kb-alias> -f "Create Your Own" --prompt "Generate a comprehensive FAQ document from all sources. Group questions by topic. For each question, provide a clear, concise answer with references to source material." -y
nlm studio status <kb-alias>
nlm download report <kb-alias> -o ./kb-faq.md
```

### If argument is `onboard`

Generate an onboarding guide:
```
nlm report create <kb-alias> -f "Study Guide" -y
nlm studio status <kb-alias>
nlm download report <kb-alias> -o ./kb-onboarding.md
```

### If argument is `summarize`

Generate a briefing of everything in the KB:
```
nlm report create <kb-alias> -f "Briefing Doc" -y
nlm studio status <kb-alias>
nlm download report <kb-alias> -o ./kb-briefing.md
```

### If argument is `share`

Make the KB publicly accessible:
```
nlm share public <kb-alias>
nlm share status <kb-alias>
```
Report the public URL.

### If argument is a question

Query the knowledge base:
```
nlm query notebook <kb-alias> "$ARGUMENTS"
```

### If no argument

List all knowledge bases:
```
nlm alias list
```
Filter for aliases starting with `kb-` and show their status.
