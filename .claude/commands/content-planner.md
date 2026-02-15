# /content-planner — Content Planning & Drafting

Aggregate source material — interviews, research, drafts, reference articles — and generate structured outlines, briefs, and drafts.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init <project-name>`

1. Create a content planner notebook:
   ```
   nlm notebook create "Content: <project-name>"
   ```
2. Register the alias:
   ```
   nlm alias set content-planner <notebook-id> -t notebook
   ```
3. Create a content brief note:
   ```
   nlm note create content-planner -c "Content project: <project-name>\nGoal: <to be filled>\nAudience: <to be filled>\nFormat: <to be filled>\nKey messages: <to be filled>" -t "Content Brief"
   ```
4. Report completion and prompt the user to add source material.

### If argument starts with `add`

Add source material to the content planner:

1. If URLs (reference articles, competitor content, inspiration):
   ```
   nlm source add content-planner --url <url> -w
   ```
2. If files (interview transcripts, drafts, notes, PDFs):
   ```
   nlm source add content-planner --file <file-path> -w
   ```
3. If inline text (raw notes, quotes, key points):
   ```
   nlm source add content-planner --text "$ARGUMENTS" --title "Notes: <summary>" -w
   ```

### If argument is `outline`

Generate a structured content outline:
```
nlm report create content-planner -f "Create Your Own" --prompt "Based on all the source material, create a detailed content outline. Include: working title, thesis/key message, section headers with bullet points for each section, key quotes or data points to include, and suggested call-to-action." -y
nlm studio status content-planner
nlm download report content-planner -o ./content-outline.md
```

### If argument is `draft`

Generate a first draft:
```
nlm report create content-planner -f "Create Your Own" --prompt "Write a complete first draft based on all the source material. Use a clear, engaging tone appropriate for the target audience. Include an introduction that hooks the reader, well-structured body sections with evidence from sources, and a strong conclusion. Cite sources where appropriate." -y
nlm studio status content-planner
nlm download report content-planner -o ./content-draft.md
```

### If argument is `angles`

Brainstorm content angles:
```
nlm query notebook content-planner "Based on all the source material, suggest 5 unique content angles or hooks. For each, explain the angle, why it would resonate with the audience, and which sources support it."
```

### If argument is a question

Query the content sources:
```
nlm query notebook content-planner "$ARGUMENTS"
```

### If no argument

Show notebook status:
```
nlm source list content-planner
nlm note list content-planner
```
