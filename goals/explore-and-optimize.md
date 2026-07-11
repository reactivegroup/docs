# Explore And Optimize Goal

## Outcome

全面探索并优化 `<workspace-root>` 中与 `kt-aicoding` 相关的项目，使每个纳入范围的仓库都有清晰定位、安装/使用路径、验证证据、远程状态记录和未解决问题说明。

## Context

- Workspace root: `<workspace-root>`
- GitHub org: `kt-aicoding`
- Scope priority: `kt-aicoding` 远程仓库及其本地 clone，优先 CLI、skill、MCP、docs/registry 项目。
- User-facing docs: 简体中文优先，除非项目已有英文规范。

Resume by reading:

- `<workspace-root>/AGENTS.md`
- this file
- `workspace/reports/PROJECTS_INVENTORY.md`
- `workspace/reports/PROJECTS_WORK_ORDERS.md`
- `workspace/reports/PROJECTS_OPTIMIZATION_QUEUE.md`
- `workspace/reports/PROJECTS_READINESS_AUDIT.md`
- `docs/audit/kt-aicoding-inventory.md` if present

## Constraints

- Never read, print, or commit secrets, tokens, cookies, `.env` values, private keys, or account credentials.
- Do not run destructive git commands.
- Do not revert user work.
- Do not publish packages, deploy production, delete repositories, create paid cloud resources, or call paid APIs without explicit user approval.
- Stage and commit only goal-related files inside individual repositories.
- If a repository has uncommitted user changes, inspect and work around them; pause if conflict is unavoidable.

## Milestones

1. Inventory `kt-aicoding` remote repositories and local clones.
2. Classify each item as active, reference, archive, blocked, or missing local clone.
3. For P0/P1 repositories, inspect README, install/use path, validation path, license, topics, and scripts.
4. Make scoped improvements with verification evidence.
5. Commit and push repo-specific changes.
6. Update audit records and run a completion audit.

## Done When

- `kt-aicoding` inventory is current.
- Each in-scope repo is recorded with local path, remote URL, branch, latest commit, status, validation evidence, and next action.
- P0 issues are fixed or recorded as acceptable blockers.
- Modified repositories have clean worktrees after push.
- Verification evidence is recorded.
- No secrets or temporary outputs are committed.

## Verification

Use narrow checks per repo:

```bash
git status --short
git log --oneline -1
```

For skill repos:

```bash
python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py skill/<name>
bash -n skill/<name>/scripts/*.sh
```

For shell/CLI repos:

```bash
bash -n scripts/*.sh bin/* tests/*.sh
bash tests/smoke.sh
```

For docs/image repos:

```bash
xmllint --noout assets/**/*.svg
bash -n scripts/*.sh
```

## If Blocked

Record blocker evidence with repo, timestamp, attempted action, exact error, owner/system, why safe work cannot continue, and next action. Continue other safe work before considering the overall goal blocked.

## Final Report

Report per repo:

```text
Repo:
Branch:
Commit:
Changes:
Validation:
Remote:
Blockers:
Next:
```
