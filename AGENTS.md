# Momentum Strategy Workspace

This repository is currently a planning and research workspace for a systematic US common-stock momentum portfolio. Application code has not been initialized.

## Current scope

- Build a local-first framework with a Python backend and responsive web frontend; future deployment must remain portable to a server.
- Use IBKR only for execution, starting with paper trading.
- Keep the investment universe separate from the defensive ETF universe.
- Preserve `openspec/` as the versioned SDD record and `.atl/skill-registry.md` as the planning index.
- Preserve `books/` as local research material; do not commit copyrighted PDFs.

## Architecture rules

- Keep market-data providers and the broker behind adapters. Do not couple investment logic to a provider or broker SDK.
- Keep broker, data-provider, and model credentials backend-only, outside version control, and never expose them to the frontend.
- Record data provenance and timestamps for any data used in analysis, backtests, or recommendations.
- Do not add broker execution, provider authentication, remote configuration, deployment, plugins, MCP servers, custom agents, or vendored skills unless separately authorized.

## Workflow and safety

- Read the relevant OpenSpec change and `openspec/config.yaml` before implementing scoped work.
- Preserve existing planning artifacts unless the active change explicitly updates them.
- Do not perform remote operations, configure remotes, push, open pull requests, or transfer files without separate user authorization.
- Use Conventional Commits and never add AI attribution or `Co-Authored-By` trailers.
- Do not invent test, build, or deployment commands. Add verified commands only when executable projects exist.
- Before any future implementation, keep changes small, verify them with applicable checks, and document unavailable checks honestly.