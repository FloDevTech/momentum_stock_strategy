# Proposal: Prepare the OpenCode Workspace

## Intent

Establish a small, portable repository boundary that OpenCode V2 can use safely before application development begins. The workspace needs shared instructions, secret hygiene, source-control rollback, and conservative tool permissions without prematurely introducing product code or workstation-specific automation.

## Scope

### In Scope

- Add a root `AGENTS.md` that states the research-only status, SDD workflow, architecture constraints, verification expectations, adapter boundaries, and secret-handling rules.
- Add a root `.gitignore` that excludes environment files, credentials, local databases, caches, build output, and generated OpenCode-local state.
- Initialize Git so future changes have an explicit repository boundary, rollback history, and worktree support.
- Add a root `opencode.jsonc` using the OpenCode V2 schema and `permissions` vocabulary, with guarded shell access and explicit protection for secrets and remote delivery.

### Out of Scope

- Application source code, project scaffolding, tests, or invented build and test commands.
- Broker or market-data integrations, custom agents, plugins, MCP servers, commands, or vendored skills.
- Provider/model credentials, user-level OpenCode authentication, deployment, or remote repository operations.
- Copying workstation-specific skill catalogs or absolute paths into the repository.

## Capabilities

### New Capabilities

- `opencode-workspace-bootstrap`: Defines the portable repository guidance, source-control boundary, secret hygiene, and guarded OpenCode V2 project configuration required before implementation.

### Modified Capabilities

None.

## Approach

Use a two-layer bootstrap. The portable layer consists of Git, `.gitignore`, and `AGENTS.md`; it carries durable project constraints independently of any AI client. The OpenCode-specific layer is a minimal `opencode.jsonc` that uses only verified V2 fields, defaults shell execution to confirmation, permits narrowly scoped read-only Git inspection, denies `git push`, and denies reads of `.env` and credential-like files.

Do not rely on OpenCode V2's currently ineffective `instructions` field to import `openspec/config.yaml` or `.atl/skill-registry.md`. Summarize mandatory constraints directly in `AGENTS.md`. Broker and data-provider credentials MUST remain backend-only, outside version control, and absent from checked-in OpenCode configuration.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `AGENTS.md` | New | Portable repository instructions and mandatory architecture, workflow, verification, and secret rules. |
| `.gitignore` | New | Exclusions for secrets, local state, databases, caches, and generated output. |
| `.git/` | New | Local source-control boundary and rollback foundation. |
| `opencode.jsonc` | New | Minimal OpenCode V2 schema and conservative project permissions. |
| `openspec/config.yaml` | Preserved | Remains the detailed SDD and product-constraint source; no requirement change. |
| `.atl/skill-registry.md` | Preserved | Remains an orchestration index and is not treated as an OpenCode skill source. |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Mixing OpenCode V1 and V2 configuration fields creates false safety expectations. | Medium | Use the V2 schema and `permissions` vocabulary only; validate configuration parsing during implementation. |
| Permission rules are too broad or fail to protect secrets and remote delivery. | Medium | Keep shell access confirmation-based, use narrow allowlists, and explicitly deny secret reads and `git push`. |
| Future credentials are committed or exposed to the frontend. | Medium | Combine `.gitignore`, OpenCode read denials, and explicit `AGENTS.md` rules requiring backend-only, uncommitted credentials. |
| Workspace guidance becomes stale when executable projects appear. | Low | Require maintainers to replace placeholder verification guidance with real commands when projects are created. |
| Git initialization is mistaken for authorization to publish remotely. | Low | State that push, pull-request creation, and remote configuration remain separate user decisions. |

## Rollback Plan

Delete `AGENTS.md`, `.gitignore`, and `opencode.jsonc` if they are unsuitable. Remove the local `.git/` directory only if no valuable commits or repository history have been created; otherwise revert the bootstrap commit while preserving history. No application data migration is involved.

## Dependencies

- OpenCode V2 configuration and permission semantics must remain compatible with the documented V2 schema.
- Git must be available locally for repository initialization.
- Provider authentication remains an external user/account concern and is not a repository dependency.

## Success Criteria

- [ ] OpenCode V2 recognizes the root workspace and accepts `opencode.jsonc` without unsupported V1 fields.
- [ ] `AGENTS.md` communicates the SDD workflow, research-only state, adapter boundary, and the rule that broker/data credentials stay backend-only and uncommitted.
- [ ] `.gitignore` covers environment files, credential-like files, local databases, caches, build output, and generated OpenCode-local state.
- [ ] OpenCode requires confirmation for general shell execution, permits only intended read-only Git inspection, denies `git push`, and blocks reads of protected secret files.
- [ ] Git reports the workspace as a repository without configuring or contacting a remote.
- [ ] No application code, integration, custom OpenCode extension, provider credential, or deployment artifact is added.
