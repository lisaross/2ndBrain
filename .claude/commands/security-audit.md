# /security-audit — Security Handbook + Codebase Audit

Build a security knowledge base from OWASP resources and stack-specific security guides, then audit your codebase against it.

**User input:** $ARGUMENTS

---

## Behavior

### If argument is `init`

1. Detect the project's tech stack (same detection as `/debug-companion`).

2. Create the security handbook notebook:
   ```
   nlm notebook create "Security Handbook — $(basename $(pwd))"
   ```

3. Register the alias:
   ```
   nlm alias set security-handbook <notebook-id> -t notebook
   ```

4. Add OWASP core resources as sources:
   ```
   nlm source add security-handbook --url "https://owasp.org/www-project-top-ten/" -w
   nlm source add security-handbook --url "https://cheatsheetseries.owasp.org/" -w
   ```

5. Add stack-specific security sources from `templates/security-sources.md`. Read the template file and add relevant URLs for the detected stack:
   ```
   nlm source add security-handbook --url <stack-specific-url> -w
   ```

6. Create a note with the project's security profile:
   ```
   nlm note create security-handbook -c "<detected stack, dependencies, exposure surface>" -t "Project Security Profile"
   ```

7. Update the Notebook Registry table in `CLAUDE.md` with the new notebook ID.

8. Report what was loaded and the notebook ID.

### If argument is `audit`

Run a full security audit of the codebase:

1. Pack the codebase:
   ```
   repomix . --output /tmp/security-audit-pack.md
   ```

2. Upload to the security handbook:
   ```
   nlm source add security-handbook --file /tmp/security-audit-pack.md -w
   ```

3. Query for each OWASP Top 10 category:
   ```
   nlm query notebook security-handbook "Analyze this codebase for A01:2021 Broken Access Control vulnerabilities"
   nlm query notebook security-handbook "Analyze this codebase for A02:2021 Cryptographic Failures"
   nlm query notebook security-handbook "Analyze this codebase for A03:2021 Injection vulnerabilities"
   ```
   Continue for all 10 categories.

4. Generate a security briefing:
   ```
   nlm report create security-handbook -f "Create Your Own" --prompt "Create a security audit report covering all OWASP Top 10 categories, listing findings by severity" -y
   nlm studio status security-handbook
   nlm download report security-handbook -o ./security-audit-report.md
   ```

5. Present findings organized by severity (Critical, High, Medium, Low).

### If argument is anything else

Treat as a specific security query:
```
nlm query notebook security-handbook "$ARGUMENTS"
```

### If no argument

Show the current state of the security handbook:
```
nlm source list security-handbook
nlm note list security-handbook
```
