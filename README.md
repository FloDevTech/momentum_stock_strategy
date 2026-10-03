# Momentum Stock Strategy

A research and planning workspace for a systematic US common-stock momentum portfolio. The project is intentionally **not an executable application yet**: this repository defines the boundaries and decisions needed to build it responsibly.

## Current status

The intended system is local-first, with a Python backend and responsive web frontend that can later be deployed to a server without coupling the investment logic to infrastructure.

There are no application packages, runnable services, test suites, or build commands in this repository yet.

## Intended product

| Area | Direction |
| --- | --- |
| Investment universe | US common stocks only |
| Defensive universe | Separate ETF universe; never mixed with the investment universe |
| Portfolio approach | Systematic momentum |
| Execution | IBKR only, beginning with paper trading |
| Architecture | Provider, broker, and model integrations behind backend adapters |
| Data handling | Record data source provenance and timestamps for analysis, backtests, and recommendations |
| Deployment | Local-first today; portable to a server later |

## Safety and architecture boundaries

- Investment logic must not depend directly on a market-data provider or broker SDK.
- Broker, data-provider, and model credentials stay backend-only, outside version control, and never reach the frontend.
- Broker execution, provider authentication, remote configuration, and deployment require separate authorization before implementation.
- Automated Yahoo data ingestion is out of scope. Data-source permissions and provenance must be considered before use.
- IBKR paper trading comes before any funded execution.

## What is here now

- `openspec/` — versioned planning and specification record.
- `.atl/skill-registry.md` — planning and skill index.
- `books/` — local research material; copyrighted PDFs must not be committed.
- `AGENTS.md` — workspace and safety instructions for contributors and coding agents.

## Contributing to the planning phase

1. Read `AGENTS.md` and the relevant OpenSpec change before proposing a change.
2. Keep planning artifacts accurate; do not introduce application scaffolding or commands that cannot be verified.
3. Preserve adapter boundaries, credential safety, and data provenance requirements.
4. Keep changes small and document checks that are unavailable because the application has not been initialized.

## Next steps

The next implementation proposal should define the first independently verifiable slice of the local-first backend while preserving the architecture and safety boundaries above.
