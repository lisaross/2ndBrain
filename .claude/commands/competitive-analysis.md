# /competitive-analysis — Competitive Intelligence

Collect competitor documentation, blog posts, product pages, and public materials. Query for comparisons, positioning, and insights.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init <market/domain>`

1. Create a competitive analysis notebook:
   ```
   nlm notebook create "Competitive Analysis: <market/domain>"
   ```
2. Register the alias:
   ```
   nlm alias set competitors <notebook-id> -t notebook
   ```
3. Run deep research on the competitive landscape:
   ```
   nlm research start "<market/domain> competitive landscape competitors comparison" -n <notebook-id> -m deep
   ```
4. Poll and import:
   ```
   nlm research status <notebook-id>
   nlm research import -n <notebook-id>
   ```
5. Create a note with initial market context:
   ```
   nlm note create competitors -c "<market overview, known competitors, positioning>" -t "Market Overview"
   ```
6. Report the number of sources found.

### If argument starts with `add`

Add competitor materials:

1. If URLs (product pages, blog posts, docs):
   ```
   nlm source add competitors --url <url> -w
   ```
2. If files (screenshots transcribed, PDFs, reports):
   ```
   nlm source add competitors --file <file-path> -w
   ```
3. If inline notes (from demos, calls, observations):
   ```
   nlm note create competitors -c "$ARGUMENTS" -t "Intel: <competitor> — <date>"
   ```

### If argument is `compare`

Generate a comparison report:
```
nlm report create competitors -f "Create Your Own" --prompt "Create a detailed competitive comparison matrix. For each competitor, cover: positioning, key features, pricing model, target audience, strengths, weaknesses, and differentiators. Include a summary of opportunities and threats." -y
nlm studio status competitors
nlm download report competitors -o ./competitive-comparison.md
```

### If argument is `landscape`

Generate a visual market map:
```
nlm mindmap create competitors -t "Competitive Landscape" -y
nlm studio status competitors
nlm download mind-map competitors -o ./competitive-landscape.json
```

### If argument is a question

Query competitive intelligence:
```
nlm query notebook competitors "$ARGUMENTS"
```

### If no argument

Show notebook status:
```
nlm source list competitors
nlm note list competitors
```
