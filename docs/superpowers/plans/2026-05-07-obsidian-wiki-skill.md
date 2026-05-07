# Obsidian Wiki Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a vault-aware Obsidian knowledge maintenance skill in this repository, with a production-quality `SKILL.md`, companion reference docs, and `agents/openai.yaml`.

**Architecture:** Treat the repository root as the final skill folder, but still use `skill-creator`'s scaffold tooling to seed the structure safely. Keep the main `SKILL.md` concise and route detailed guidance into `references/` files. Position the skill as an orchestration layer that depends on Obsidian companion skills for execution.

**Tech Stack:** Markdown, YAML, Python utility scripts from `skill-creator`, git, GitHub

---

### Task 1: Scaffold the skill structure

**Files:**
- Create: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold/obsidian-wiki-skill/`
- Modify: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/`

- [ ] **Step 1: Create a temporary scaffold with the official initializer**

```bash
mkdir -p /Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold
python3 /Users/wenweikun/.codex/skills/.system/skill-creator/scripts/init_skill.py \
  obsidian-wiki-skill \
  --path /Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold \
  --resources references \
  --interface display_name="Obsidian Wiki Skill" \
  --interface short_description="Vault-aware Obsidian knowledge maintenance" \
  --interface default_prompt='Use $obsidian-wiki-skill to maintain my Obsidian knowledge vault.'
```

Expected: a scaffold directory at `/Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold/obsidian-wiki-skill/` with `SKILL.md`, `agents/openai.yaml`, and `references/`.

- [ ] **Step 2: Inspect the generated scaffold before copying anything**

Run:

```bash
find /Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold/obsidian-wiki-skill -maxdepth 3 -type f | sort
```

Expected: includes `SKILL.md`, `agents/openai.yaml`, and a `references/` directory. No scripts or assets are needed in v1.

- [ ] **Step 3: Verify the repository root remains the final skill home**

Use this structure target:

```text
/Users/wenweikun/workspace/project_obsidian-wiki-skill/
├── SKILL.md
├── agents/openai.yaml
├── references/
│   ├── workflow-modes.md
│   ├── evidence-and-safety.md
│   └── companion-skill-routing.md
└── docs/
    └── superpowers/
```

- [ ] **Step 4: Commit the scaffolding checkpoint**

```bash
git add docs/superpowers/plans/2026-05-07-obsidian-wiki-skill.md
git commit -m "docs: add implementation plan for obsidian wiki skill"
```

Expected: one commit that preserves the plan before content implementation starts.

### Task 2: Write the root `SKILL.md`

**Files:**
- Create: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/SKILL.md`
- Reference: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/docs/superpowers/specs/2026-05-07-obsidian-vault-aware-knowledge-skill-design.md`

- [ ] **Step 1: Write a failing shape check by asserting the file does not yet exist**

Run:

```bash
test -f /Users/wenweikun/workspace/project_obsidian-wiki-skill/SKILL.md
```

Expected: exit status `1` before creation.

- [ ] **Step 2: Write the frontmatter and top-level sections**

Create `SKILL.md` with this structure:

```markdown
---
name: obsidian-wiki-skill
description: Maintain and evolve Obsidian-based knowledge vaults using a host-aware workflow for orientation, source ingest, answering, and audit. Use when Codex needs to work inside an existing Obsidian vault or Markdown knowledge system to connect source notes, knowledge notes, project notes, and system notes; maintain schema/index/log conventions; or run vault-aware knowledge maintenance with required companion skills such as obsidian-markdown, obsidian-cli, obsidian-bases, and json-canvas.
---

# Obsidian Wiki Skill

## Mission

## Required Companion Skills

## Operating Principles

## Modes

## Orientation Workflow

## Information Model

## Ingest Workflow

## Answer Workflow

## Audit Workflow

## Evidence And Safety Policy

## Write Safety Policy
```

- [ ] **Step 3: Fill the body with the approved orchestration behavior**

Use these content requirements:

```markdown
- Define the skill as a vault-aware orchestration layer, not a fixed-folder wiki generator.
- Require `obsidian-markdown`, `obsidian-cli`, `obsidian-bases`, and `json-canvas`.
- Treat `defuddle` as optional but recommended.
- Make `orient` and `answer` read-only by default.
- Make `ingest` and `audit` the only write-capable modes.
- Explain that note roles matter more than folder names.
- Define `SCHEMA.md`, `index.md`, and `log.md` as protocol roles rather than mandatory root files.
- Add write-risk thresholds: low risk (1-2 notes), medium risk (3+ notes), high risk (10+ notes).
- Add source trust and prompt-injection guardrails.
```

- [ ] **Step 4: Run a readability check on the new file**

Run:

```bash
sed -n '1,260p' /Users/wenweikun/workspace/project_obsidian-wiki-skill/SKILL.md
```

Expected: complete frontmatter, no placeholder text, and a concise body that delegates detailed procedures to `references/`.

- [ ] **Step 5: Commit the main skill draft**

```bash
git add /Users/wenweikun/workspace/project_obsidian-wiki-skill/SKILL.md
git commit -m "feat: add core obsidian wiki skill"
```

### Task 3: Add detailed reference docs

**Files:**
- Create: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/references/workflow-modes.md`
- Create: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/references/evidence-and-safety.md`
- Create: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/references/companion-skill-routing.md`

- [ ] **Step 1: Write `references/workflow-modes.md`**

Create this outline:

```markdown
# Workflow Modes

## orient
- anchor-first orientation
- structure probing fallback
- local topic search only after orientation

## answer
- vault-only vs externally verified answers
- no automatic filing

## ingest
- source-first writes
- cautious promotion into knowledge/project notes
- update index/log only when the vault already uses them or the change is material

## audit
- structure, navigation, metadata, relationship, and evidence review
```

- [ ] **Step 2: Write `references/evidence-and-safety.md`**

Create this outline:

```markdown
# Evidence And Safety

## Evidence Strength
- direct
- derived
- weak
- unverified

## Query Pollution Guardrail

## Source Trust

## Conflict Handling

## Write Safety Thresholds
```

- [ ] **Step 3: Write `references/companion-skill-routing.md`**

Create this outline:

```markdown
# Companion Skill Routing

## obsidian-markdown
When to invoke it and what it owns

## obsidian-cli
When to invoke it and what it owns

## obsidian-bases
When to invoke it and what it owns

## json-canvas
When to invoke it and what it owns

## defuddle
When to invoke it and how it fits before ingest
```

- [ ] **Step 4: Verify all reference files exist and are internally consistent**

Run:

```bash
find /Users/wenweikun/workspace/project_obsidian-wiki-skill/references -maxdepth 1 -type f | sort
rg -n "TODO|TBD|placeholder" /Users/wenweikun/workspace/project_obsidian-wiki-skill/references
```

Expected: the three files exist and `rg` returns no matches.

- [ ] **Step 5: Commit the references**

```bash
git add /Users/wenweikun/workspace/project_obsidian-wiki-skill/references
git commit -m "docs: add reference guides for obsidian wiki skill"
```

### Task 4: Generate `agents/openai.yaml`

**Files:**
- Create: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/agents/openai.yaml`

- [ ] **Step 1: Create the `agents/` directory**

Run:

```bash
mkdir -p /Users/wenweikun/workspace/project_obsidian-wiki-skill/agents
```

Expected: `agents/` exists at repository root.

- [ ] **Step 2: Generate the UI metadata from the skill**

Run:

```bash
python3 /Users/wenweikun/.codex/skills/.system/skill-creator/scripts/generate_openai_yaml.py \
  /Users/wenweikun/workspace/project_obsidian-wiki-skill \
  --interface display_name="Obsidian Wiki Skill" \
  --interface short_description="Vault-aware Obsidian knowledge maintenance" \
  --interface default_prompt='Use $obsidian-wiki-skill to maintain my Obsidian knowledge vault.'
```

Expected: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/agents/openai.yaml` is created or refreshed.

- [ ] **Step 3: Smoke-check the generated YAML**

Run:

```bash
sed -n '1,200p' /Users/wenweikun/workspace/project_obsidian-wiki-skill/agents/openai.yaml
```

Expected: contains `interface.display_name`, `interface.short_description`, and a default prompt that explicitly mentions `$obsidian-wiki-skill`.

- [ ] **Step 4: Commit the agent metadata**

```bash
git add /Users/wenweikun/workspace/project_obsidian-wiki-skill/agents/openai.yaml
git commit -m "chore: add skill UI metadata"
```

### Task 5: Validate, clean up, and publish

**Files:**
- Modify: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/.gitignore`
- Delete: `/Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold/`

- [ ] **Step 1: Add scaffold cleanup coverage to `.gitignore` if needed**

Ensure `.gitignore` contains:

```gitignore
.DS_Store
.scaffold/
```

- [ ] **Step 2: Run validation**

Run:

```bash
python3 /Users/wenweikun/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  /Users/wenweikun/workspace/project_obsidian-wiki-skill
```

Expected: validation passes. If the local Python environment is missing `yaml`, switch to an environment that includes `PyYAML` before retrying.

- [ ] **Step 3: Run final manual checks**

Run:

```bash
git status --short
sed -n '1,220p' /Users/wenweikun/workspace/project_obsidian-wiki-skill/SKILL.md
sed -n '1,200p' /Users/wenweikun/workspace/project_obsidian-wiki-skill/agents/openai.yaml
```

Expected: only intended files changed, no placeholders, and the skill reads clearly from top to bottom.

- [ ] **Step 4: Remove the temporary scaffold**

```bash
rm -rf /Users/wenweikun/workspace/project_obsidian-wiki-skill/.scaffold
```

- [ ] **Step 5: Commit and push the finished skill**

```bash
git add .gitignore SKILL.md agents/openai.yaml references
git commit -m "feat: add vault-aware obsidian wiki skill"
git push origin main
```

## Self-Review

### Spec coverage

- Skill positioning, activation boundary, host-first orientation, operating modes, information model, evidence policy, write safety, source trust, conflict policy, and companion-skill routing are all covered across Tasks 2-5.
- Strong dependency on Obsidian companion skills is implemented in Task 2 and expanded in Task 3.
- The final repository shape stays aligned with the approved spec.

### Placeholder scan

- No `TODO`, `TBD`, or "implement later" instructions remain in the plan steps.
- Each step includes exact file paths or commands.

### Type consistency

- The planned skill name is consistently `obsidian-wiki-skill`.
- The same companion skill names and reference file names are used throughout the plan.
