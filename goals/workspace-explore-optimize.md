# Workspace Explore And Optimize Goal

## Outcome

对 `<workspace-root>` 下所有可发现项目进行全面探索、分层优先级排序、低风险优化、验证和交付记录。最终每个项目必须处于以下状态之一:

- `optimized`: 已完成本轮可执行优化，并有本地/线上验证证据。
- `healthy-no-change`: 当前健康，无需本轮修改，并有当前证据。
- `needs-follow-up`: 发现问题但不适合本轮自动修改，有明确下一步。
- `externally-blocked`: 被权限、平台、DNS、生产数据、付费服务或用户 dirty 改动阻塞，有 blocker record。
- `archive/docs-only`: 资料/归档类项目，只做结构、说明、链接和归档口径检查。
- `not-applicable`: 非项目、生成物、缓存、第三方样例或无需维护对象。

本目标不是只做扫描报告；应在安全范围内逐个项目完成可验证优化，包括 README/部署说明/env example/脚本入口/域名台账/LLM provider 状态/CI 或本地验证修复等低风险改进。涉及生产部署、数据库 schema、付费操作、强制覆盖或 secret 暴露时暂停并记录 blocker。

## Workdir

`<workspace-root>`

## Must Read Before Continuing

每次开始、恢复或上下文压缩后，先读取当前状态，不依赖旧聊天记忆:

1. `<workspace-root>/AGENTS.md`
2. `<workspace-root>/workspace/reports/PROJECTS_INVENTORY.md`
3. `<workspace-root>/workspace/reports/PROJECTS_INVENTORY.json`
4. `<workspace-root>/archive/2026-06/workspace-audits/PROJECTS_RECHECK_AUDIT.md`
5. `<workspace-root>/archive/2026-06/workspace-audits/PROJECTS_RECHECK_AUDIT.json`
6. `<workspace-root>/workspace/reports/PROJECTS_DOMAIN_CHECKS.md`
7. `<workspace-root>/workspace/reports/PROJECTS_READINESS_AUDIT.md`
8. `<workspace-root>/workspace/reports/PROJECTS_WORK_ORDERS.md`
9. `<workspace-root>/workspace/reports/PROJECTS_MAINTENANCE.md`
10. 若存在，读取本目标台账:
    - `<workspace-root>/archive/2026-06/workspace-audits/PROJECTS_EXPLORE_OPTIMIZE_LEDGER.md`
    - `<workspace-root>/archive/2026-06/workspace-audits/PROJECTS_EXPLORE_OPTIMIZE_COMPLETION_AUDIT.md`

处理单个项目时，按就近优先级读取:

1. `AGENTS.md`
2. `CLAUDE.md`
3. `README.md`
4. `DEPLOYMENT.md` / `DEPLOY.md`
5. `package.json` / `pyproject.toml` / `go.mod` / `Cargo.toml` / `pom.xml`
6. `.github/workflows/*`
7. Vercel、Supabase、CloudBase、Railway、Netlify、Cloudflare、Docker 配置线索

## Scope

In scope:

- `<workspace-root>` 下所有 inventory 可发现 Git 仓库、嵌套 Git 仓库、非 Git 包项目和线上/部署项目。
- 重点覆盖 GitHub repo、dirty repo、带线上域名项目、带部署配置项目、AI/LLM 项目、近期维护项目、用户入口项目。
- 可做低风险优化: 文档补齐、README 当前状态、部署说明、env example 名称补齐、验证脚本说明、台账更新、小型 lint/test 明确修复、旧 provider runtime 线索确认、域名状态记录。
- 可做非破坏性验证: lint、test、typecheck、build、HTTP smoke、API health smoke、浏览器 smoke、CLI dry-run、日志只读检查。

Out of scope unless user confirms:

- 生产部署或流量切换。
- 删除远端 env、改生产数据库 schema、迁移生产数据。
- 付费外部服务调用或高成本模型调用。
- 强推、reset、回滚用户改动、大规模重构。
- 输出、复制、提交真实 secret/token/cookie/API key。

## Priority

按以下顺序处理:

1. P0: `blocked` 项、线上域名异常项、dirty 很重且有部署/用户入口的项目。
2. P1: GitHub + Vercel/Supabase/CloudBase/Cloudflare + AI/LLM/runtime 项目。
3. P2: 活跃 Web/App/工具项目，有明确 README 和验证脚本。
4. P3: MCP/CLI/SDK/基础设施项目。
5. P4: 资料库、知识库、归档项目，只做归档口径、README、链接和结构检查。
6. P5: non-git/package-only 项目，确认是否应纳入 Git、归档或标记 not-applicable。

## Core Rules

1. 保护 secrets: 只记录 secret 名称、env var 名、平台名或“需要权限”，不打印真实值。
2. 保护 dirty worktree: 修改前记录 `git status --short`; 不要回滚用户改动; 只 stage 本目标相关文件。
3. 一个项目一个闭环: 探索、优化、验证、提交/记录、更新台账，再进入下一个项目。
4. 不为“有提交”制造无关改动。
5. 使用项目现有包管理器和脚本，不随意替换 npm/pnpm/yarn/uv/go/maven 流程。
6. 文档和台账是权威续跑入口，每完成一批必须更新。
7. 缺少权限不停止全局目标; 记录 blocker 后继续其他项目。
8. 不把历史资料库中的旧 provider 文档误判为 runtime 风险; 必须区分 runtime 代码、env example、历史文档、锁文件和生成物。

## Milestones

1. Baseline: 重新刷新 inventory、domain checks、readiness、dirty 和 LLM provider 线索，确认项目总数和优先级。
2. P0/P1 Optimization: 处理 blocked、域名异常、部署项目、AI/LLM 项目的安全可执行优化。
3. Validation: 对可验证项目运行最窄有意义验证; 线上项目运行 HTTP/API/browser smoke。
4. Delivery: 对实际修改过的项目只提交相关文件，推送到 tracked branch，并确认 remote ref。
5. Completion Audit: 更新根台账和完成审计，证明所有项目均已分类、验证或记录 blocker。

## Per-Project Loop

1. Inventory:
   - 记录 path、repo、branch、upstream、latest commit、dirty/untracked 数量。
   - 识别 GitHub remote、部署平台、域名、技术栈、包管理器、验证脚本、AI/LLM provider 线索。

2. Targeted Reads:
   - 读取项目本地说明和配置。
   - 对大型资料库优先 `rg` 定位，不全文扫无关内容。

3. Decide:
   - 判断本项目本轮目标: 优化、健康无改动、需跟进、外部阻塞、归档、或不适用。
   - 明确最小可完成改动，避免重构扩散。

4. Optimize:
   - 优先补齐 README 当前状态、运行/验证命令、部署说明、env example 名称、域名说明、Ark/LLM provider 状态。
   - 可修复小型 lint/test/doc/link/config 问题。
   - 不做破坏性清理、大规模重构或生产变更。

5. Validate:
   - Web: 优先 `lint`/`typecheck`/`build`，必要时启动 dev server 做浏览器 smoke。
   - API/后端: 优先测试、健康接口、CLI dry-run。
   - Python: 优先 `uv run` 或项目文档指定流程。
   - Go/Java/Rust: 优先项目已有 test/build。
   - 域名: HTTP HEAD/GET、关键 API health、必要时 browser smoke。
   - 高成本、需权限或可能写生产的验证只记录建议命令和 blocker。

6. Commit/Push:
   - 只在项目内实际修改代码/文档/配置时执行。
   - 运行 `git diff --check`。
   - 只 stage 本项目相关文件。
   - commit message 使用清晰范围，例如 `docs: update project maintenance notes`。
   - push 到 tracked branch，并确认 remote ref。
   - 根目录台账若不在 Git 仓库，则记录为本地台账更新，不做 commit。

7. Ledger:
   - 更新 `<workspace-root>/archive/2026-06/workspace-audits/PROJECTS_EXPLORE_OPTIMIZE_LEDGER.md`。
   - 每项记录: 状态、证据、命令、结果、commit、remote ref、域名 smoke、blocker、下一步。

## Blocker Policy

如果遇到以下情况，完成安全本地工作后记录 blocker，并继续其他项目:

- GitHub/Vercel/Supabase/CloudBase/Railway/Cloudflare 未登录或权限不足。
- 域名 DNS、证书、托管项目归属需要平台确认。
- 测试依赖生产 secret、真实支付、付费模型或外部高成本调用。
- 需要数据库 schema/生产数据/远端 env 修改。
- 用户 dirty 改动影响验证，且不能安全隔离。
- 项目依赖缺失或构建耗时过长，超出本轮合理验证成本。

每个 blocker 必须记录:

- project
- owner/system
- timestamp
- attempted action
- current error/result
- why safe local work cannot continue
- next action
- whether it blocks global completion

只有当所有剩余项目都被同一个外部条件卡住，且连续多轮无法产生新证据，才可将整个 goal 标记 blocked。

## Verification

全局验证要求:

1. 运行并记录全量项目枚举命令。
2. 刷新或核对 `PROJECTS_INVENTORY.*`。
3. 对所有域名项目运行 HTTP/API smoke，记录 OK/CHECK。
4. 对所有 P0/P1 项目运行适合的本地验证或记录明确 blocker。
5. 对所有修改过的项目运行 `git diff --check`。
6. 对提交过的项目确认 remote ref。
7. 对新增/更新台账运行 secret/key 形态扫描，确认无真实 secret。
8. 对 UI/线上关键项目，能安全浏览器验证时记录浏览器 smoke 结果。
9. 对 LLM/AI 项目区分 Ark runtime、旧 GLM runtime、env example、历史文档和锁文件命中。

## Done When

只有全部条件满足时才能 mark complete:

1. `<workspace-root>` 下所有可发现项目均已进入 ledger，并有状态分类。
2. P0/P1 项目均已优化、验证、提交/记录，或有合格 blocker。
3. 所有线上域名均有当前 HTTP/API/browser smoke 结果或 blocker。
4. 所有 dirty 项目至少记录 dirty 影响范围; 被修改项目没有混入无关改动。
5. 所有 AI/LLM 项目都有 provider 状态证据，旧 provider runtime 风险已处理或记录。
6. 根目录台账已更新:
   - `archive/2026-06/workspace-audits/PROJECTS_EXPLORE_OPTIMIZE_LEDGER.md`
   - `archive/2026-06/workspace-audits/PROJECTS_EXPLORE_OPTIMIZE_COMPLETION_AUDIT.md`
   - 必要时同步 `archive/2026-06/workspace-audits/PROJECTS_RECHECK_AUDIT.md`、`workspace/reports/PROJECTS_DOMAIN_CHECKS.md`、`workspace/reports/PROJECTS_WORK_ORDERS.md`
7. 新增/更新文件通过 secret/key 形态扫描。
8. Completion audit 逐项证明 scope、验证、提交、域名、blocker、secrets 都覆盖。
9. 最终报告列出总数、分类数、优化项目数、提交项目数、域名结果、失败验证、阻塞项和下一批建议。

## Completion Audit

完成前创建或更新:

`<workspace-root>/archive/2026-06/workspace-audits/PROJECTS_EXPLORE_OPTIMIZE_COMPLETION_AUDIT.md`

必须包含:

- 当前项目总数和来源命令。
- 每个 explicit requirement 的证据位置。
- P0/P1 项目的完成表。
- 域名 smoke 汇总。
- 本地验证汇总。
- Git commit/push/remote ref 汇总。
- blocker records。
- secret/key 扫描结果。
- 未完成但可接受的外部阻塞说明。
- 明确结论: 是否允许 mark complete。

## Final Report

最终回复必须简洁列出:

- 总项目数、GitHub repo 数、域名数。
- optimized / healthy-no-change / needs-follow-up / externally-blocked / archive/docs-only / not-applicable 数量。
- 修改并提交的项目、branch、commit、remote ref。
- 线上验证和本地验证结果。
- 仍需用户授权或平台处理的 blocker。
- 最优先的下一批工作。
