# Prepare OpenCode Workspace

## Objective
Create a portable, guarded workspace bootstrap so application implementation can be performed from OpenCode.

## Problem
The workspace currently contains only research material and SDD planning artifacts. It lacks repository-level instructions, secret hygiene, Git history, and OpenCode V2 project configuration.

## Scope
- Create `AGENTS.md`, `.gitignore`, and `opencode.jsonc`.
- Initialize a local Git repository.
- Preserve existing `books/`, `openspec/`, and `.atl/` artifacts.

## Constraints
- No application source code, broker/data integration, provider credentials, remote configuration, push, or deployment.
- Credentials remain backend-only and uncommitted.
- OpenCode configuration uses V2 fields only and conservatively requests shell actions.
- Authored change budget: approximately 400 lines; delivery strategy: ask-on-risk.

## TDD
- Mode: disabled (no executable project or workspace test command exists).
- Verification: configuration parse/readback, Git state, and credential-ignore checks.

## Tasks
- [x] OWS-01 — Create portable workspace guidance and OpenCode V2 configuration. Route: delegated; trigger: multiple non-trivial files. Acceptance: `AGENTS.md`, `.gitignore`, and `opencode.jsonc` exist; configuration parses as JSONC after comments are removed; the rules preserve secret and remote safeguards.
- [x] OWS-02 — Initialize Git and commit the bootstrap. Route: delegated; trigger: execution command and work-unit commit. Acceptance: local repository with one Conventional Commit; no remote configured.

## Progress
- Current state: bootstrap completed locally; application code remains intentionally out of scope.
- Evidence: OpenCode V2 configuration follows the official `permissions` / `shell` vocabulary; shell defaults to confirmation, routine local Git inspection is allowed, `git push` is denied, secrets are denied, and external directories are not granted.
- Verification: readback and JSONC parse completed; Git repository, no-remote state, ignore patterns, and staged file scope checked before commit.
- Engram mirror: pending because the memory transport was unavailable during local planning.

## Next Step
Create and approve the first product-scoped planning change before adding executable application code.