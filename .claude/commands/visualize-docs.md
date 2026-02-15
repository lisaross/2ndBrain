# /visualize-docs — Visual Artifacts from Notebooks

Generate mind maps, infographics, slide decks, data tables, and reports from any registered notebook.

**User input:** $ARGUMENTS

Expected format: `<notebook-alias> <artifact-type>`

---

## Behavior

### Parse arguments

- First argument: notebook alias (e.g., `second-brain`, `debug-companion`)
- Second argument: artifact type — one of `mindmap`, `infographic`, `slides`, `table`, `report`, `audio`, `all`

If no arguments provided, default to `second-brain all`.

### Artifact generation

#### `mindmap`
```
nlm mindmap create <notebook-alias> -t "Mind Map: <alias>" -y
nlm studio status <notebook-alias>
nlm download mind-map <notebook-alias> -o ./artifacts/<alias>-mindmap.json
```

#### `infographic`
```
nlm infographic create <notebook-alias> -y
nlm studio status <notebook-alias>
nlm download infographic <notebook-alias> -o ./artifacts/<alias>-infographic.png
```

#### `slides`
```
nlm slides create <notebook-alias> -y
nlm studio status <notebook-alias>
nlm download slide-deck <notebook-alias> -o ./artifacts/<alias>-slides.pdf
```

#### `table`
```
nlm data-table create <notebook-alias> -y
nlm studio status <notebook-alias>
nlm download data-table <notebook-alias> -o ./artifacts/<alias>-table.csv
```

#### `report`
```
nlm report create <notebook-alias> -f "Briefing Doc" -y
nlm studio status <notebook-alias>
nlm download report <notebook-alias> -o ./artifacts/<alias>-report.md
```

#### `audio`
```
nlm audio create <notebook-alias> -y
nlm studio status <notebook-alias>
nlm download audio <notebook-alias> -o ./artifacts/<alias>-audio.mp3
```

#### `all`

Generate all artifact types above in sequence. Wait for each to complete before starting the next.

### Steps

1. Create `./artifacts/` directory if it doesn't exist.
2. Verify the notebook alias resolves:
   ```
   nlm alias get <notebook-alias>
   ```
3. Generate requested artifact(s) using commands above.
4. For each artifact, poll `nlm studio status` until complete.
5. Download completed artifacts to `./artifacts/`.
6. Report all generated files with their paths.
