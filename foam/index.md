# Project memory

Map of Content (MOC). Start here before product or architecture decisions.

## How to use

1. **New feature** → `cda-prd` → `prd/PRD-NNN-slug.md`, link ADRs.
2. **Implementation** → `cda-plan` → `plans/PLAN-NNN-slug.md`.
3. **Technical choice** → `foam/decisions/ADR-NNN-slug.md`.
4. **Sync kanban** → `import-kanban.sh` refreshes [[features/shipped|shipped]] / [[features/backlog|backlog]].

## Product

- [[product/vision|Vision & positioning]]

## Features

- [[features/index|Feature catalog]]
- [[features/shipped|Shipped]]
- [[features/backlog|Backlog]]
- [[features/out-of-scope|Out of scope]]

## Architecture

- [[architecture/must-haves|Must-haves (v0 intent)]]
- [[architecture/os-landscape|Mobile OS landscape (research)]]
- [[architecture/nfc-contactless-payments|NFC contactless payments]]

## Decisions (ADRs)

Index: [[decisions/index|All ADRs]]

| ID | Title | Status |
| -- | ----- | ------ |
| [[decisions/ADR-001-curated-device-set\|ADR-001]] | Curated device set | proposed |

## PRDs & plans

| PRD | Status |
| --- | ------ |
| _(none yet)_ | |

- PRD template: `prd/template.md`
- Plan template: `plans/template.md`

## Tags

`#product` `#architecture` `#deployment` `#data` `#auth`
