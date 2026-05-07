# Obsidian Wiki Skill

A vault-aware knowledge maintenance skill for Obsidian-based Markdown systems.

This project turns the LLM Wiki idea into a more practical skill for real Obsidian vaults. Instead of assuming a fixed wiki folder structure, it starts by understanding the user's existing vault and then works through four modes: `orient`, `answer`, `ingest`, and `audit`.

## Why This Exists

The original `llm-wiki` pattern is strong on the core idea of persistent, compounding knowledge. In practice, many Obsidian users already have their own vault structure, templates, indexes, and note taxonomy. A good skill should adapt to that reality instead of forcing a brand-new information architecture.

This skill is designed to:

- respect existing vault structure and naming habits
- treat Obsidian as the host environment
- distinguish source preservation from knowledge synthesis
- avoid silently promoting chat answers into stable vault knowledge
- add stronger evidence, safety, and write-discipline rules
- route low-level execution to dedicated Obsidian companion skills

## What The Skill Does

This skill acts as an orchestration layer for Obsidian knowledge work.

It decides:

- what mode the current request belongs to
- whether the task should remain read-only or become a write workflow
- which note layer should receive new information
- which Obsidian companion skill should perform the concrete operation

It does not try to replace low-level Obsidian syntax or CLI skills.

## Core Modes

- `orient`: understand the vault before acting
- `answer`: answer from vault context without writing by default
- `ingest`: add new source material and selectively promote durable knowledge
- `audit`: review structure, navigation, metadata, relationships, and evidence quality

## Design Principles

- Host-first: read the existing vault before making assumptions
- Role-first: infer note roles from `type`, purpose, templates, and relationships rather than folder names alone
- Conservative by default: keep `orient` and `answer` read-only
- Evidence-aware: treat source notes as the evidence layer and knowledge notes as the conclusion layer
- Write-safe: require planning for medium-risk writes and confirmation for high-risk writes
- Companion-skill driven: use dedicated Obsidian skills for concrete format and vault actions

## Required Companion Skills

This skill depends on the following execution-layer skills:

- `obsidian-markdown`
- `obsidian-cli`
- `obsidian-bases`
- `json-canvas`

Recommended:

- `defuddle`

If those skills are unavailable, this skill should not pretend to offer complete Obsidian-native behavior.

## Repository Layout

```text
.
├── SKILL.md
├── README.md
├── agents/openai.yaml
├── references/
│   ├── workflow-modes.md
│   ├── evidence-and-safety.md
│   └── companion-skill-routing.md
└── docs/
    ├── SKILL.md
    ├── karpathy-llm-wiki.md
    ├── upgrade.md
    └── superpowers/
```

## Key Files

- [SKILL.md](SKILL.md): the actual skill definition
- [agents/openai.yaml](agents/openai.yaml): UI metadata for the skill
- [references/workflow-modes.md](references/workflow-modes.md): detailed behavior for `orient`, `answer`, `ingest`, and `audit`
- [references/evidence-and-safety.md](references/evidence-and-safety.md): evidence policy, source trust, conflict handling, and write safety
- [references/companion-skill-routing.md](references/companion-skill-routing.md): when to invoke each companion Obsidian skill
- [docs/SKILL.md](docs/SKILL.md): original upstream skill used as a baseline
- [docs/karpathy-llm-wiki.md](docs/karpathy-llm-wiki.md): the core idea document
- [docs/upgrade.md](docs/upgrade.md): analysis of what needed to change

## Installation

This repository is the skill folder.

Place it where your Codex environment can discover skills, for example:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s /path/to/obsidian-wiki-skill "${CODEX_HOME:-$HOME/.codex}/skills/obsidian-wiki-skill"
```

Or copy the folder directly into your skills directory.

## Usage

Use this skill when you want Codex to work inside an existing Obsidian vault as a knowledge maintainer rather than a generic editor.

Example prompts:

- `Use $obsidian-wiki-skill to orient to my Obsidian vault before we make changes.`
- `Use $obsidian-wiki-skill to ingest this article into my source and knowledge notes.`
- `Use $obsidian-wiki-skill to audit my vault for weak evidence and navigation drift.`
- `Use $obsidian-wiki-skill to answer this question from my vault without writing back.`

## Validation

The skill was validated with the `skill-creator` quick validator.

If you want to re-run validation locally:

```bash
PYTHONPATH=/path/to/vendor/python python3 /path/to/skill-creator/scripts/quick_validate.py /path/to/obsidian-wiki-skill
```

## Status

This is an initial public version focused on:

- host-aware Obsidian orientation
- safe source ingest
- conservative answer behavior
- evidence and write-discipline rules
- strong composition with Obsidian companion skills

Future iterations can add helper scripts, forward tests, and more opinionated audit automation if repeated workflows justify them.
