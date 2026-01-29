## citepaper

A Codex skill that creates BibTeX citations from short paper keywords or a cue like `bib: ...`. It looks up authoritative sources, formats authors as "Last, First", and removes long fields like abstracts. It also supports fast mode and source flags for quicker retrieval.

## How to use it
1) Clone or copy this skill into your Codex skills directory (for example, inside `~/.codex/skills`).
2) Start Codex and use the skill in chat.
3) Specify additional formatting, e.g., remove url. 
4) Update references.bib with results.

Example usage:

Inside codex CLI

```
bib:"denoising diffusing models" 2021 source:dblp mode:fast
```

Notes:
- `source:` and `mode:` are optional.
- alternatives: source:arxiv|openreview|acm|ieee|springer
