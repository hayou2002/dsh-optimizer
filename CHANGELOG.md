# Changelog

## 0.1.0 - 2026-10-31

首个 DSH 适配版本，自 `codex-optimizer` 0.4.1 派生。

- 命名与路径迁移到 DSH：`$DSH_HOME` / `~/.dsh`、`.optimize/dsh-rules.json`、`dsh_optimizer.py`，并保留对旧 `codex-optimizer` 注入标记与旧保护名的迁移兼容。
- 保护名单改为 DSH 真实状态面：`.credentials.yaml`、`.env`、`.anonymous-user-id`、`prompt-inject.md`、`workspace.json`、`sessions/`、`attachments/`、`storages/`、`cache/`、`logs/`、`profiles/`、`skills/`、`integrations/`、`channel-pack/`、`.plugin-backups/`、`.agent-presets/` 与运行数据库。
- 项目发现改为**会话传入的项目根**（`--project-root`）与工作区现场，不再假定存在可读的原生项目列表；规则文件字段由 `managedRoots` 换成 `trustedRoots`。
- 知识治理改写：DSH 没有原生 `/memories` 控制面，长期知识落在 `$DSH_HOME/AGENTS.md`、`~/.agents/AGENTS.md`、技能与项目文档。
- 自动化改写为 DSH 的 `schedule_create` / `schedule_list` / `schedule_update` / `schedule_delete` 参数模型（`delivery` 必填，六选一选择器，可选权限与模型）。
- 文档与示例统一为 bash（`$HOME/...`、`export PYTHONUTF8=1`），去掉 PowerShell 语法。
- 参考章节按 DSH 现实校正，`references/04` 与 `references/05` 整体重写。

## 上游 codex-optimizer 历史

以下条目继承自上游 `codex-optimizer` 的 CHANGELOG，随本包一起保留，方便对照派生点（0.4.1）。
DSH 侧版本号从 0.1.0 重新起算，与上游编号不连续。

### 0.4.1 - 2026-10-26

- Replace the fixed five-item environment check with action-scoped evidence.
- Stop running a full read-only diagnostic after initialization.
- Avoid hashing cleanup candidates during plan creation when the digest is not
  used by the trash transaction.
- Unify phase validation under one verification budget.

### 0.4.0 - 2026-10-26

- Add `organize-scan` for a single read-only inventory during `03`.
- Make project documentation repair demand-driven instead of applying it to all
  historical projects.
- Preserve private or runtime process data in a grouped high-risk recovery
  transaction instead of forcing it through low-risk automatic cleanup.
- Replace unconditional ten-step reference synchronization with targeted checks
  based on whether paths and project identity actually changed.

### 0.3.0 - 2026-10-26

- Add `archive-batch` for same-volume archival of legacy recovery batches that
  already carry manifests.
- Skip invalid legacy batches instead of restarting or hand-repairing the whole
  archive operation.
- Collapse repeated diagnostics, temporary helper compilation, transaction
  repair, and duplicate verification into one execution with one result check.

### 0.2.0 - 2026-10-26

- Add `quick-project` for explicit local and Git project adoption.
- Keep the full plan, hash, and rollback transaction for destructive or risky operations.
- Keep a concise project `AGENTS.md` while skipping empty `work/`/`outputs/` trees.
- Require collaboration leases only for actual overlap or handoffs.
- Use size and mtime validation for copies and staging; reserve SHA256 and extra backups for destructive, conflict, or release paths.
- Correct collaboration and diagnostic CLI examples.

### 0.1.0 - 2026-10-26

- First Codex-native release.
- Adds the initialization, optimize, tidy, and overview workflows.
- Adds standard-library diagnostics and rollbackable apply/rollback transactions.
- Adds project promotion, reference repair, cache recovery, memory curation, and automation templates.
- Adds Codex and Hanako shared-root leases, handoffs, conflict rules, and checkpoints.
- Establishes isolation from the original Hanako optimizer.
