# Paper Hub

Personal research paper library with structured annotations, a journal club tracker, and multi-format citation export. Single-file web app, no backend.

**Live site:** https://leomeow123.github.io/paper-hub/

## What it does

- **Library** – two-line rows with title, authors, year, journal, model, region, tags, and key findings. Facet sidebar (tags, model, project, status, year), full-text search, and sort by recently added, year, title, journal, or status.
- **Journal Club** – papers marked for journal club, split into upcoming and past, with presentation date, presenter, and inline discussion notes that save automatically.
- **Add Paper** – paste a DOI, publisher URL, or PubMed link to auto-fill metadata from Crossref, then add species, region, tags, methods, findings, and notes. Inputs suggest values already in the library.
- **Detail view** – full record with citation export in Nature, Cell, Science, or BibTeX format. Arrow keys move between papers.
- **Batch Claude** – generates a prompt to fill missing metadata for many papers at once and applies the returned JSON.
- **Import / Export** – JSON or BibTeX in, JSON out. Duplicates are skipped by DOI or title.

## How data is stored

`papers.json` in this repo is the single source of truth. The app loads it through the GitHub API when a token is configured (gear icon, top right), and writes edits back as commits. Without a token it falls back to a local cache and then the static file, in read-only mode.

To sync from a new device, create a fine-grained GitHub token with **Contents: read and write** on this repo and paste it into the sync settings.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole app: markup, styles, and script |
| `papers.json` | The library, one object per paper |

## Paper record

```json
{
  "id": "paller-2017-tmr-sleep",
  "title": "...",
  "authors": "Last, F.M.; Last, F.M.",
  "year": "2017",
  "journal": "Current Directions in Psychological Science",
  "doi": "10.1177/0963721417716928",
  "species": "human",
  "region": "sleep, memory consolidation",
  "tags": ["journal club", "sleep", "memory", "review"],
  "methods": "...",
  "status": "unread",
  "project": "",
  "funding": "",
  "abstract": "...",
  "findings": "1-3 sentence summary",
  "notes": "why it matters",
  "journalClub": { "date": "2026-10-03", "presenter": "", "discussion": "" },
  "added": "2026-09-28"
}
```

`status` is `unread`, `reading`, or `read`. `journalClub` is present only on journal club papers. Authors are separated by semicolons so the citation exporter can split them.

## Local development

Any static server works:

```bash
python3 -m http.server 8000
# open http://localhost:8000/
```
