# Workflow Modes

## `orient`

Use `orient` when:

- entering a vault for the first time in a session
- resuming after a long context gap
- the request is ambiguous
- the request references a vault but does not yet justify writing

Work in this order:

1. Read anchor files such as `SCHEMA.md`, `index.md`, `log.md`, `AGENTS.md`, and vault guide notes.
2. Probe the vault structure only if the anchors are missing or incomplete.
3. Infer the active note roles, stable frontmatter fields, and navigation system.
4. Decide whether the next step belongs to `answer`, `ingest`, or `audit`.

Default rule:

- `orient` is read-only

## `answer`

Use `answer` when the user wants understanding rather than file changes.

Answer flow:

1. Decide whether the vault alone is enough.
2. Read the smallest relevant set of source, knowledge, project, and system notes.
3. Distinguish between source-backed facts, vault-level synthesis, and claims that still need fresh verification.
4. Answer clearly and conservatively.

Default rule:

- do not create or update notes unless the user explicitly asks

## `ingest`

Use `ingest` when the user wants new material folded into the vault.

Ingest flow:

1. Identify the current source-note convention.
2. Preserve the new material in the source layer first.
3. Decide whether the source justifies changes to knowledge or project notes.
4. Update indexes, dashboards, or log notes only when that matches the vault's existing habits or clearly improves navigation.
5. Summarize exactly what changed.

Default rule:

- do not spread a single source across many notes unless the value is clear

## `audit`

Use `audit` when the user wants to check vault health or repair maintenance drift.

Audit scope:

- structure
- navigation
- metadata
- relationships
- evidence traceability
- duplication
- stale or weak synthesis

Default rule:

- read first, then propose or apply targeted fixes

### `lint` sub-mode

Treat `lint` as the default sub-mode inside `audit`.

Use it when the user asks to:

- lint the vault
- run a health check
- find navigation drift
- inspect weak evidence
- check schema, index, or log consistency

Lint checklist:

- structure health
- navigation health
- metadata coverage
- relationship quality
- evidence traceability
- stale or weak synthesis
- schema, index, or log drift when those files exist

Default rule:

- report findings first
- do not repair automatically unless the user asks for fixes or the task already includes repair
