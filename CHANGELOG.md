# Changelog

## 9.0.0 (2026-05-18)

- **Section 0: User State Assessment** — Before entering pre-loading, assess user intent
  - 🟢 Clear: proceed to project breakdown
  - 🟡 Fuzzy: engage in dialogue first, do not output phase breakdown
  - Examples table for common fuzzy-intent scenarios
- Renumbered all sections (0→1, 1→2, ..., 7→8, 8→9)
- What to Avoid: added "pre-loading before user state assessment" anti-pattern

## 4.0.0 (2026-05-17)

- Full bilingual (EN/ZH) specification throughout
- Decision tree for task type classification (ASCII flowchart)
- 8 standardized task types with phase definitions, actions, outputs, and completion criteria
- Formal agent behavior specification: first response, transition protocol, allowed operations
- Edge case handling table (7 scenarios with resolution rules)
- Removed all internal/private information from public content
- Professionally curated README with ClawHub metadata

## 1.0.0 (2026-05-17)

- Initial release: basic plan mode with workspace creation and requirements gathering
- Auto-trigger detection for complex tasks
- Manual trigger via keywords ('plan mode', etc.)
