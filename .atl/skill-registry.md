# Skill Registry

Generated during SDD initialization. This is an index; read the referenced `SKILL.md` before using a skill.

## Skills

| Name | Trigger / description | Scope | Source |
| --- | --- | --- | --- |
| chained-pr | Trigger: PRs over 400 lines, stacked PRs, review slices. Split oversized changes into chained PRs that protect review focus. | user | `C:/Users/FLODEV/.codex/skills/chained-pr/SKILL.md` |
| cognitive-doc-design | Design docs that reduce cognitive load. Trigger: writing guides, READMEs, RFCs, onboarding, architecture, or review-facing docs. | user | `C:/Users/FLODEV/.codex/skills/cognitive-doc-design/SKILL.md` |
| go-testing | Trigger: Go tests, go test coverage, Bubbletea teatest, golden files. Apply focused Go testing patterns. | user | `C:/Users/FLODEV/.codex/skills/go-testing/SKILL.md` |
| imagegen | Generate or edit raster images when the task benefits from AI-created bitmap visuals such as photos, illustrations, textures, sprites, mockups, or transparent-background cutouts. Use when Codex should create a brand-new image, transform an existing image, or derive visual variants from references, and the output should be a bitmap asset rather than repo-native code or vector. Do not use when the task is better handled by editing existing SVG/vector/code-native assets, extending an established icon or logo system, or building the visual directly in HTML/CSS/canvas. | user | `C:/Users/FLODEV/.codex/skills/.system/imagegen/SKILL.md` |
| judgment-day | Trigger: judgment day, dual review, adversarial review, juzgar. Run explicit blind dual review with at most two scoped fix/re-judgment rounds. | user | `C:/Users/FLODEV/.codex/skills/judgment-day/SKILL.md` |
| openai-docs | Use for Codex models/pricing, scheduled tasks, skills, settings, setup, troubleshooting, customization, automations, and self-knowledge—including | user | `C:/Users/FLODEV/.codex/skills/.system/openai-docs/SKILL.md` |
| review-agent | Perform a read-only, defect-first review of a specified code change and return every actionable finding. Use when another agent delegates review of uncommitted changes, a base-branch diff, a commit, or custom review instructions. | user | `C:/Users/FLODEV/.codex/skills/.system/review-agent/SKILL.md` |
| skill-creator | Create or update a Codex skill with appropriately scoped instructions and any needed supporting resources. | user | `C:/Users/FLODEV/.codex/skills/.system/skill-creator/SKILL.md` |
| skill-improver | Trigger: improve skills, audit skills, refactor skills, skill quality. Audit and upgrade existing LLM-first skills. | user | `C:/Users/FLODEV/.codex/skills/skill-improver/SKILL.md` |
| skill-installer | Install Codex skills into $CODEX_HOME/skills from a curated list or a GitHub repo path. Use when a user asks to list installable skills, install a curated skill, or install a skill from another repo (including private repos). | user | `C:/Users/FLODEV/.codex/skills/.system/skill-installer/SKILL.md` |
| work-unit-commits | Plan commits as reviewable work units. Trigger: implementation, commit splitting, chained PRs, or keeping tests and docs with code. | user | `C:/Users/FLODEV/.codex/skills/work-unit-commits/SKILL.md` |

## Project Conventions

No physical project convention files were found during initialization.
