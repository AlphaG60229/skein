# Changelog

## v1.0.0 — 2026-07-05

Initial release.

- Single-file, zero-dependency Markdown knowledge graph viewer for Chromium browsers.
- Named workspaces: save multiple folders, rename, forget, one-click resume of the last one.
- Force-directed graph with cooling simulation, node dragging, pan/zoom, fit, focus, relayout.
- YAML frontmatter parsing, wikilink + `related:` edges, faceted filters, debounced full-text search.
- Full Markdown rendering: headings, bold/italic, ordered & unordered lists, blockquotes (with
  nested inline formatting), GFM-style tables with column alignment, fenced code blocks with
  lightweight dependency-free syntax highlighting, and local images resolved via File System
  Access (network image URLs are blocked by CSP, by design).
- View tab with backlinks, in-place editor with unsaved-changes guard, note creation from template.
- Lint report: filename/id mismatch, broken wikilinks, duplicate ids, orphans, missing fields.
- Security: full HTML escaping, CSP with `connect-src 'none'`, read-only permission by default.
- Persistent UI preferences (theme, panel layout).
- Bilingual README (English + Traditional Chinese).
