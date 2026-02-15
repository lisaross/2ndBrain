# NLM CLI Reference (v0.2.18)

Complete command reference for the `nlm` CLI — a command-line interface for Google NotebookLM.

**Install:** `npm install -g @nichochar/nlm`
**Auth:** `nlm login`
**Health check:** `nlm doctor`

---

## Notebooks

### Create a notebook
```bash
nlm notebook create "<name>"
```
Returns the notebook ID.

### List all notebooks
```bash
nlm notebook list
```

### Get notebook details
```bash
nlm notebook get <notebook-id>
```

### AI-generated notebook summary
```bash
nlm notebook describe <notebook-id>
```

### Query a notebook
```bash
nlm notebook query <notebook-id> "<question>"
# Alias:
nlm query notebook <notebook-id> "<question>"
```

---

## Sources

### Add a website or YouTube URL
```bash
nlm source add <notebook-id> --url <url> -w
```
`-w` waits for processing to complete.

### Upload a local file
```bash
nlm source add <notebook-id> --file <path> -w
```
Supported: PDF, MD, TXT, and other text formats.

### Add inline text
```bash
nlm source add <notebook-id> --text "<content>" --title "<title>" -w
```

### Add a Google Drive document
```bash
nlm source add <notebook-id> --drive <google-doc-id> -w
```

### List sources
```bash
nlm source list <notebook-id>
```

### Delete a source
```bash
nlm source delete <notebook-id> <source-id>
```

### Check for stale Drive sources
```bash
nlm source stale <notebook-id>
```

### Sync stale sources
```bash
nlm source sync <notebook-id>
```

---

## Notes

### Create a note
```bash
nlm note create <notebook-id> -c "<content>" -t "<title>"
```

### List notes
```bash
nlm note list <notebook-id>
```

### Update a note
```bash
nlm note update <notebook-id> <note-id> -c "<new content>"
```

### Delete a note
```bash
nlm note delete <notebook-id> <note-id>
```

---

## Query & Research

### Query a notebook
```bash
nlm query notebook <notebook-id> "<question>"
```

### Query specific sources
```bash
nlm query notebook <notebook-id> "<question>" -s <source-id-1>,<source-id-2>
```

### Continue a conversation
```bash
nlm query notebook <notebook-id> "<question>" -c <conversation-id>
```

### Start fast research (~30s, 10 sources)
```bash
nlm research start "<query>" -n <notebook-id> -m fast
```

### Start deep research (~5min, 40+ sources)
```bash
nlm research start "<query>" -n <notebook-id> -m deep
```

### Check research status
```bash
nlm research status <notebook-id>
```

### Import discovered sources
```bash
nlm research import -n <notebook-id>
```

---

## Visualizations & Artifacts

### Mind map
```bash
nlm mindmap create <notebook-id> -t "<title>" -y
```

### Infographic
```bash
nlm infographic create <notebook-id> -y
```

### Slide deck
```bash
nlm slides create <notebook-id> -y
```

### Data table
```bash
nlm data-table create <notebook-id> -y
```

### Briefing document
```bash
nlm report create <notebook-id> -f "Briefing Doc" -y
```

### Study guide
```bash
nlm report create <notebook-id> -f "Study Guide" -y
```

### Custom report
```bash
nlm report create <notebook-id> -f "Create Your Own" --prompt "<prompt>" -y
```

### Podcast-style audio
```bash
nlm audio create <notebook-id> -y
```

### Check artifact generation status
```bash
nlm studio status <notebook-id>
```

`-y` auto-confirms the creation prompt.

---

## Downloads

### Mind map (JSON)
```bash
nlm download mind-map <notebook-id> -o <output-path>
```

### Report (Markdown)
```bash
nlm download report <notebook-id> -o <output-path>
```

### Infographic (PNG)
```bash
nlm download infographic <notebook-id> -o <output-path>
```

### Slide deck (PDF)
```bash
nlm download slide-deck <notebook-id> -o <output-path>
```

### Data table (CSV)
```bash
nlm download data-table <notebook-id> -o <output-path>
```

### Audio (MP3)
```bash
nlm download audio <notebook-id> -o <output-path>
```

---

## Sharing

### Make notebook public
```bash
nlm share public <notebook-id>
```

### Make notebook private
```bash
nlm share private <notebook-id>
```

### Invite a collaborator
```bash
nlm share invite <notebook-id> --email <email>
```

### Check sharing status
```bash
nlm share status <notebook-id>
```

---

## Aliases

### Set an alias
```bash
nlm alias set <alias-name> <notebook-id> -t notebook
```

### Resolve an alias
```bash
nlm alias get <alias-name>
```

### List all aliases
```bash
nlm alias list
```

### Delete an alias
```bash
nlm alias delete <alias-name>
```

---

## Utility

### Login / authenticate
```bash
nlm login
```

### Check login status
```bash
nlm login --check
```

### Run diagnostics
```bash
nlm doctor
```

### Check version
```bash
nlm --version
```
