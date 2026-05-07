# Companion Skill Routing

## `obsidian-markdown`

Use `obsidian-markdown` when writing or editing Obsidian notes that depend on:

- wikilinks
- embeds
- callouts
- frontmatter properties
- Obsidian-flavored Markdown details

This skill owns note-format correctness.

## `obsidian-cli`

Use `obsidian-cli` when the task needs:

- vault search
- note creation or append actions
- property reads or writes
- backlinks or tag inspection
- interaction with a running Obsidian instance

This skill owns live vault operations.

## `obsidian-bases`

Use `obsidian-bases` when working with `.base` files, structured note views, filters, formulas, or Base-powered dashboards.

This skill owns `.base` schema correctness.

## `json-canvas`

Use `json-canvas` when creating or editing `.canvas` files, note maps, or visual canvases.

This skill owns `.canvas` structure and edge/node integrity.

## `defuddle`

Use `defuddle` before ingest when a webpage should become a clean Markdown source note.

Use it to reduce clutter and preserve the source layer in a vault-friendly format.

If `defuddle` is unavailable, state that limitation before using a weaker fallback.
