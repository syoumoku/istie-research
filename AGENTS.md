# iSite Agents

## Project goal
Build a source-first, evidence-first workflow for country-scale property discovery, evidence enrichment, and white-box scoring.

## Five-module SOP
1. Scope definition
2. Discovery and entity resolution
3. Evidence processing and standardization
4. Value assessment
5. Delivery

## Source of truth
- `skills/SKILL.md`: main operating spec
- `skills/PLAYBOOK.md`: quick execution guide
- `skills/scoring_rules.md`: scoring rules
- `skills/scenario_capacity_models.md`: scenario metric rules
- `skills/proxy_rules.md`: proxy and evidence constraints
- `skills/output_templates.md`: Excel/PPT minimum output schemas

## Agent roles
- `orchestrator`: reads manifests and delegates work
- `source-expander`: expands source registry by country and scenario
- `discovery-worker`: builds raw candidate universe
- `resolver`: deduplicates and resolves entities
- `evidence-builder`: fills standardized evidence slots
- `scoring-worker`: computes white-box scores from standardized evidence
- `qa-reviewer`: checks evidence breaks, duplicate scoring, and proxy misuse
- `delivery-worker`: builds Excel/PPT deliverables

## Editable directories by agent
- `source-expander` -> `sources/registry/`, `docs/`
- `discovery-worker` -> `data/bronze/`, `docs/`
- `resolver` -> `data/silver/`, `docs/`
- `evidence-builder` -> `data/silver/`, `reviews/`
- `scoring-worker` -> `data/gold/`, `reviews/`
- `delivery-worker` -> `deliverables/`

## Hard rules
- Never skip evidence standardization before scoring.
- Never collapse all sources into one free-text note.
- Never score directly from raw webpages.
- Never overwrite bronze raw records.
- Never remove source traceability.
- Do not force a fixed top-N output per country.
