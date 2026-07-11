# kt-aicoding Inventory Audit

Updated: 2026-06-28 Asia/Shanghai

Scope: `<workspace-root>` local clones and `kt-aicoding` GitHub organization.

## Summary

- Remote repositories: 16
- Local clones found: 16
- Newly cloned this run: `agent-workflows`, `kt-aicoding-dotgithub`
- Workspace reports refreshed with `python3 tools/project_workspace_inventory.py --root <workspace-root>`
- Registry updated and pushed: `kt-aicoding/registry@8e5e3b3`
- Existing unrelated dirty clone observed and not modified: `<workspace-root>/cloud/.github` (`capa-cloud/.github`)

## Remote To Local Map

| Remote repo | Local path | Branch | Latest local commit | Worktree | Status | Next action |
| --- | --- | --- | --- | --- | --- | --- |
| `kt-aicoding/.github` | `<workspace-root>/skills/kt-aicoding-dotgithub` | `main` | `447e162` Rename statusline kit to cc codex config | clean | active/reference | Review org profile in a later pass |
| `kt-aicoding/agent-workflows` | `<workspace-root>/agent-workflows` | `main` | `e0e0cd2` docs: add reusable workflow templates | clean | verified | Planning, pre-landing review, and multi-agent research workflow templates added; diff and sensitive scans passed |
| `kt-aicoding/agents` | `<workspace-root>/agents` | `main` | `8cb0c4c` docs: optimize agents knowledge base | clean | verified | Local HEAD matches remote `main`; no current dirty worktree |
| `kt-aicoding/claudecode-codex-config` | `<workspace-root>/cli/claudecode-codex-config` | `main` | `26bf9ba` fix: add dry run for config installer | clean | verified | Installer has `--dry-run`; README dev validation uses dry-run/temp install; unit tests and temp install passed |
| `kt-aicoding/claudecode-codex-switch` | `<workspace-root>/cli/claudecode-codex-switch` | `main` | `a9466e0` docs: make Ark the default ccuse path | clean | verified | Smoke test, shell syntax, README SVG validation passed; remote main verified through GitHub API |
| `kt-aicoding/claws` | `<workspace-root>/claws` | `main` | `060ea1e` Document known OpenClaw machine candidate | clean | reference | No immediate action |
| `kt-aicoding/cli-tools` | `<workspace-root>/cli/cli-tools` | `main` | `bec1dee` docs: complete Cloudflare resource snapshot | clean | verified | README validation entrypoint and Chinese related-skill links added; Cloudflare resource snapshot completed; diff/sensitive scans passed |
| `kt-aicoding/hermes` | `<workspace-root>/hermes` | `main` | `18d7939` docs: add optimization goal and safety scanner | clean | verified | Local HEAD matches remote `main`; no current dirty worktree |
| `kt-aicoding/images` | `<workspace-root>/knowledge/images` | `main` | `83c4223` docs: add project image usage guide | clean | verified | README includes project-type image usage guide; SVG and export script validated |
| `kt-aicoding/mcp-servers` | `<workspace-root>/mcp/mcp-servers` | `main` | `127fc1a` docs: add MCP governance validation | clean | verified | README validation entrypoint and Chinese related-skill links added; diff/sensitive scans passed |
| `kt-aicoding/registry` | `<workspace-root>/registry` | `main` | `8e5e3b3` docs: record workflow and browser skill validation | clean | verified | Registry catalog, goal file, exploration ledger, and platform cost reference updated and pushed this run |
| `kt-aicoding/skill-goal` | `<workspace-root>/skills/skill-goal` | `main` | `6bf2895` docs: add one-line goal skill install | clean | verified | One-line install added; skill structure validated |
| `kt-aicoding/skill-image` | `<workspace-root>/skills/skill-image` | `main` | `4a7f215` docs: add one-line skill install | clean | verified | One-line install added; skill structure and helper script validated |
| `kt-aicoding/skill-jd` | `<workspace-root>/skills/skill-jd` | `main` | `57d2590` docs: harden JD skill install guidance | clean | verified | Install/update command hardened; `AGENTS.md` added; skill validator, shell syntax, and destructive-command refusal checks passed |
| `kt-aicoding/skill-taobao` | `<workspace-root>/skills/skill-taobao` | `main` | `e07bdab` docs: harden Taobao skill install guidance | clean | verified | Install/update command hardened; `.gitignore` added; skill validator, shell syntax, and destructive-command refusal checks passed |
| `kt-aicoding/skills` | `<workspace-root>/skills/kt-aicoding-skills` | `main` | `0e16658` docs: add skills install and safer goal guidance | clean | verified | One-line install and validation loop added; goal-prompt-builder secret guidance tightened; all Codex skills validated |

## Verification Evidence This Run

```bash
env -u GH_TOKEN gh repo list kt-aicoding --limit 200 --json name,url,description,visibility,updatedAt
python3 tools/project_workspace_inventory.py --root <workspace-root>
env -u GH_TOKEN gh api repos/kt-aicoding/registry/contents/catalog/exploration-optimization-ledger.md --jq '.name + " " + .sha + " " + .html_url'
```

For newly created image-related repositories in the previous turn:

```bash
python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py <workspace-root>/skills/skill-image/skill/skill-image
bash -n <workspace-root>/skills/skill-image/skill/skill-image/scripts/recommend-image-tool.sh
xmllint --noout <workspace-root>/knowledge/images/assets/examples/readme-assets-workflow.svg
bash -n <workspace-root>/knowledge/images/scripts/export-svg.sh
<workspace-root>/knowledge/images/scripts/export-svg.sh <workspace-root>/knowledge/images/assets/examples <workspace-root>/knowledge/images/tmp/examples
```

For this README optimization pass:

```bash
python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py <workspace-root>/skills/skill-image/skill/skill-image
bash -n <workspace-root>/skills/skill-image/skill/skill-image/scripts/recommend-image-tool.sh
python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py <workspace-root>/skills/skill-goal/goal-prompt
bash -n <workspace-root>/knowledge/images/scripts/export-svg.sh
xmllint --noout <workspace-root>/knowledge/images/assets/examples/readme-assets-workflow.svg
<workspace-root>/knowledge/images/scripts/export-svg.sh <workspace-root>/knowledge/images/assets/examples <workspace-root>/knowledge/images/tmp/examples
git ls-remote origin main
env -u GH_TOKEN gh api repos/kt-aicoding/<repo>/contents/README.md --jq '.html_url + " " + .sha'
```

For the config/switch pass:

```bash
python3 -m unittest
python3 scripts/install.py --help
python3 scripts/install.py --dry-run
CLAUDE_DIR="$tmp/claude" CODEX_HOME="$tmp/codex" KT_AICODING_CONFIG_HOME="$tmp/local" python3 scripts/install.py
bash tests/smoke.sh
bash -n bin/ccuse bin/codexuse scripts/install.sh
xmllint --noout assets/readme/overview.svg assets/readme/config-flow.svg
env -u GH_TOKEN gh api repos/kt-aicoding/claudecode-codex-config/contents/scripts/install.py --jq '.html_url + " " + .sha'
env -u GH_TOKEN gh api repos/kt-aicoding/claudecode-codex-switch/commits/main --jq '.sha + " " + .commit.message'
```

For the governance repo pass:

```bash
git diff --check
rg -n "gho_|Bearer|SERVICE_ROLE|password|cookie|secret|token|API_KEY|/Users/" README.md README.zh-CN.md docs || true
for skill in skills/codex/*; do
  python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py "$skill"
done
env -u GH_TOKEN gh api repos/kt-aicoding/cli-tools/contents/README.zh-CN.md --jq '.html_url + " " + .sha'
env -u GH_TOKEN gh api repos/kt-aicoding/mcp-servers/contents/README.zh-CN.md --jq '.html_url + " " + .sha'
env -u GH_TOKEN gh api repos/kt-aicoding/skills/contents/skills/codex/goal-prompt-builder/SKILL.md --jq '.html_url + " " + .sha'
git ls-remote origin main
```

For the shopping skill and workflow pass:

```bash
python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py <workspace-root>/skills/skill-jd
bash -n <workspace-root>/skills/skill-jd/scripts/pw-jd.sh
<workspace-root>/skills/skill-jd/scripts/pw-jd.sh close
python3 <codex-home>/skills/.system/skill-creator/scripts/quick_validate.py <workspace-root>/skills/skill-taobao
bash -n <workspace-root>/skills/skill-taobao/scripts/pw-taobao.sh
<workspace-root>/skills/skill-taobao/scripts/pw-taobao.sh close
git -C <workspace-root>/agent-workflows diff --check
env -u GH_TOKEN gh api repos/kt-aicoding/agent-workflows/contents/workflows/planning/repo-optimization.md --jq '.html_url + " " + .sha'
env -u GH_TOKEN gh api repos/kt-aicoding/skill-jd/contents/README.md --jq '.html_url + " " + .sha'
env -u GH_TOKEN gh api repos/kt-aicoding/skill-taobao/contents/README.md --jq '.html_url + " " + .sha'
git ls-remote origin main
```

For the final remote SHA audit:

```bash
env -u GH_TOKEN gh repo list kt-aicoding --limit 200 --json name,url,visibility,updatedAt --jq 'sort_by(.name)[] | [.name,.visibility,.url,.updatedAt] | @tsv'
env -u GH_TOKEN gh api "repos/kt-aicoding/<repo>/commits/main" --jq '.sha'
```

All 16 local HEADs matched GitHub REST `main` commit SHAs on 2026-06-28.

## Blockers / Deferrals

| Item | Reason | Next action |
| --- | --- | --- |
| `<workspace-root>/cloud/.github` | Existing local clone is `capa-cloud/.github`, not `kt-aicoding/.github`; has untracked `AGENTS.md`. | Keep untouched; use `<workspace-root>/skills/kt-aicoding-dotgithub` for kt-aicoding org profile. |
| Private billing dashboards | Exact invoices, payment details, and billing usage dollars were not inspected to avoid private account data in public docs. | Use provider dashboards with the user present if exact billing figures are needed. |
| Railway | `railway whoami` reported unauthorized in the platform pass. | Run `railway login` only when Railway checks are needed. |

## Next Batch Candidates

1. Optional: review `kt-aicoding/.github` organization profile copy and screenshots.
2. Optional: do a focused future pass on `claws`, `agents`, and `hermes` if their product direction changes.
3. User-present: exact provider billing dashboards if current dollar spend is required.

## Completion Audit

- [x] Objective file and `docs/goals/explore-and-optimize.md` reread after resume.
- [x] `kt-aicoding` remote inventory enumerated from current GitHub state: 16 public repositories.
- [x] All 16 `kt-aicoding` local clones are present and clean on `main`.
- [x] All 16 local HEADs match GitHub REST `main` commit SHAs.
- [x] P0/P1 public install/use paths for config, switcher, skills, MCP, CLI, images, workflows, and registry have validation evidence.
- [x] Modified repositories were committed, pushed, and remote-verified.
- [x] Workspace reports refreshed with `python3 tools/project_workspace_inventory.py --root <workspace-root>`.
- [x] Sensitive scans were run for changed public docs; matches were safety text, placeholders, or false positives such as `tokenizer`, not raw credentials.
- [x] Remaining items are classified as optional future review, private billing dashboard follow-up, Railway auth follow-up, or unrelated non-`kt-aicoding` dirty clone.
