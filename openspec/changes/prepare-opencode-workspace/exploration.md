## Exploration: Prepare OpenCode Workspace

### Current State
The workspace is a research-only SDD bootstrap. It contains `openspec/`, `.atl/skill-registry.md`, and source books, but no application source, root agent instructions, OpenCode project configuration, or Git repository. The initialized product constraints require future broker and market-data credentials to remain backend-only and integrations to sit behind adapters.

OpenCode V2 does not require a project configuration file to start, but its supported repository guidance is a root `AGENTS.md`. A root `opencode.jsonc` is the correct place for project-scoped safety policy. OpenCode V2 accepts an `instructions` array but does not currently load those entries, so relying on that field to import the existing SDD files would silently fail. Project skills are discovered from `.opencode/skills/` or compatible `.agents/skills/`; the current `.atl/skill-registry.md` is only an index and is not itself an OpenCode skill source.

Official references:
- [OpenCode V2 configuration](https://opencode.ai/v2/docs/config)
- [OpenCode V2 instructions](https://opencode.ai/v2/docs/instructions)
- [OpenCode V2 permissions](https://opencode.ai/v2/docs/permissions)
- [OpenCode V2 skills](https://opencode.ai/v2/docs/skills)
- [OpenCode V2 providers](https://opencode.ai/v2/docs/providers)

### Affected Areas
- `openspec/config.yaml` — existing portable SDD context; preserve as the source for current architecture and credential constraints.
- `.atl/skill-registry.md` — existing SDD-generated index; useful to humans and orchestration, but not automatically consumed by OpenCode.
- `AGENTS.md` — planned portable repository guidance; should summarize architecture, workflow, verification, and secret-handling rules directly because OpenCode V2 loads this file.
- `opencode.jsonc` — planned OpenCode-specific configuration; should contain the schema and a small, explicit permission policy only.
- `.gitignore` — planned portable repository hygiene; should exclude environment files, credentials, local databases, caches, build output, and OpenCode-local state if generated.
- `.opencode/skills/` — optional planned OpenCode-specific extension point; add only project-owned skills that are actually needed, rather than copying the global Codex skill catalog or hard-coding user-specific absolute paths.
- `.git/` — planned generic source-control boundary; not required merely to launch OpenCode, but strongly recommended before implementation for change isolation, rollback, and reliable project/worktree behavior.

### Approaches
1. **Minimal portable core plus guarded OpenCode config** — add root `AGENTS.md`, `.gitignore`, initialize Git, and add a small `opencode.jsonc` with V2 schema and conservative permissions.
   - Pros: Clear project boundary; portable instructions; explicit safety; no duplicated or stale skill bundle; smallest maintainable setup.
   - Cons: Requires a later proposal/design to define exact permission rules and repository instructions; user-level provider setup remains external.
   - Effort: Low

2. **OpenCode-heavy workspace bundle** — additionally create custom agents, commands, plugins, and vendored skills under `.opencode/` immediately.
   - Pros: Rich workflow automation from the first implementation session.
   - Cons: Premature without source layout or test commands; duplicates global tooling; increases maintenance and permission surface; risks encoding V1 fields instead of current V2 fields.
   - Effort: Medium

3. **No repository files; rely on global OpenCode defaults** — start OpenCode in the directory and configure everything per user globally.
   - Pros: Zero workspace changes.
   - Cons: Product constraints are not reliably shared; safety depends on one machine; the current SDD registry is not auto-loaded; poor reproducibility.
   - Effort: Low

### Recommendation
Use approach 1. The proposal should define a two-layer bootstrap:

1. **Portable workspace layer:** initialize Git; add `.gitignore`; add a concise root `AGENTS.md` that names the SDD workflow, current research-only state, backend-only credential rule, adapter boundary, strict prohibition on committing secrets, and the rule that test/build commands must be updated after the real projects exist.
2. **OpenCode-specific layer:** add root `opencode.jsonc` using the V2 schema and V2 `permissions` vocabulary. Default shell execution to `ask`, allow routine read-only Git inspection, deny `git push`, deny reads of `.env` and credential-like files, and avoid provider/model credentials in the repository. Provider authentication should remain in OpenCode's account/environment mechanisms, not checked-in configuration.

Do not add custom agents, plugins, MCP servers, commands, or vendored skills yet. Add a project skill later only when a stable workflow exists that cannot be expressed clearly in `AGENTS.md`. Do not use the currently ineffective V2 `instructions` field as a bridge to `openspec/config.yaml` or `.atl/skill-registry.md`; summarize mandatory constraints in `AGENTS.md` instead.

### Risks
- OpenCode V1 and V2 documentation use different configuration shapes; mixing `permission`/`bash`/`task` with V2 `permissions`/`shell`/`subagent` would create a misleading safety configuration.
- Without Git initialization, repository boundaries, rollback, and later worktree-based workflows remain weak even though OpenCode can still open the directory.
- Broad shell or external-directory allowances would expose the host user's filesystem and network authority; the official permissions guide recommends narrow allowlists.
- Copying the global Codex skill catalog into `.opencode/skills/` would couple the project to one workstation and could create duplicate skill IDs with precedence surprises.
- The workspace has no executable project or test command yet, so implementation agents must not invent verification commands or claim TDD readiness.
- Product and broker secrets could leak if future `.env`, IBKR, or data-provider files are not denied in OpenCode permissions and excluded by `.gitignore`.

### Ready for Proposal
Yes. The next phase should propose only the workspace bootstrap artifacts and their acceptance checks. Application scaffolding, product behavior, broker/data integration, model selection, user-level provider login, and deployment remain out of scope.
