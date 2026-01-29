---
name: citepaper
description: 'Create BibTeX citations from short paper keywords or a cue like "bib: ...". Use when the user asks for a BibTeX entry, citation, or reference and expects web lookup/verification, multiple candidate disambiguation, and author names formatted as "Last, First".'
---

# Cite paper

## Overview
Resolve paper keywords into verified BibTeX entries using web sources, returning clean BibTeX with author names formatted as "Last, First" and no abstract field.

## Workflow

### 1) Parse the request
- If the user provides `bib: ...`, treat the remainder as search keywords.
- If the request is underspecified (e.g., only a short phrase), ask for one disambiguator (year, venue, or author) before searching.
- If the user specifies a preferred venue/version (e.g., ICLR, arXiv), prioritize that.

### 2) Web lookup (required)
- Use `web.run` search queries to find authoritative BibTeX entries.
- Prefer primary sources in this order when available:
  1) Official venue/publisher pages (OpenReview, ACM, IEEE, Springer, arXiv)
  2) DBLP
  3) Institutional repositories or author pages
- Cross-check title, year, and authors across sources.
- If a term looks unfamiliar or ambiguous, search explicitly for that term.

### 3) Candidate handling
- If multiple plausible matches exist, present 2–4 concise options (title, venue, year, first author) and ask the user to choose.
- Only proceed to finalize the BibTeX entry after the user selects a candidate.

### 4) Build the BibTeX entry
- Required fields to include when available: `author`, `title`, `booktitle` or `journal`, `year`, `publisher`, `url`, `doi`, `pages`, `month`, and any standard venue-specific fields (e.g., `volume`, `number`).
- Remove `abstract` and other long text fields unless explicitly requested.
- Author formatting: `Last, First` and joined by ` and `.
- Title capitalization: preserve proper nouns with braces `{}` as needed.
- Use a key pattern like `lastnameYYYYshorttitle` unless the user requests a specific key.

### 5) Respond
- Output only the BibTeX block(s) in a fenced code block unless the user asks for commentary.
- If offering multiple candidates, present short descriptions and wait for selection.
- Include citations for factual statements derived from web sources.
- Do not include raw URLs in prose; only inside code blocks (e.g., the `url` field).
- If no definitive match is found, summarize what was found and why it was insufficient, then ask for more details.
