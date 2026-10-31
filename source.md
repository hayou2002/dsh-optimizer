# Project Sources

- Project slug: `dsh-optimizer`
- Primary edit location: `C:\Users\Administrator\Desktop\OH-WorkSpace\projects\dsh-optimizer`
- Shared workspace: `C:\Users\Administrator\Desktop\OH-WorkSpace`
- Collaborating Agents: DSH and Hanako
- Upstream package: `codex-optimizer`（Codex 适配版，Codex/Hanako 共享根治理）
- Upstream lineage: `https://github.com/hayou2002/hana-optimizer`（泛化 PR #1）→ `codex-optimizer` → 本包
- Frozen upstream copy: `projects/dsh-optimizer/src/codex-optimizer/`（只读对照）
- Adapted: 2026-10-31

## 本包是什么

`dsh-optimizer` 是 DSH 侧的治理 skill：把清理与整理做成可回滚的文件事务，管理治理根的项目、规则、技能、自动化、知识载体与工作目录，并严格保护 DSH 主目录中的认证与运行状态。

DSH 适配的主要口径变化见 `CHANGELOG.md` 的 0.5.0 段，要点是：

- `CODEX_HOME`/`~/.codex` → `DSH_HOME`/`~/.dsh`；规则文件 `.optimize/dsh-rules.json`。
- 保护名单改为 DSH 真实状态面（凭据、会话、附件、存储、缓存、日志、profile、技能、集成、插件备份与运行数据库）。
- 项目发现改为会话传入的 `--project-root` 与工作区现场，不假定存在可读的原生项目列表。
- 知识治理不再假定原生 `/memories` 控制面；自动化改为 DSH 的 `schedule_*` 参数模型。
- 示例统一为 bash；`build_release.py` 的运行时清单以本包实际文件为准。

## Migrated material

- DSH skill 入口（`SKILL.md`）、配置模板、参考章节 01–08、执行器脚本、发布打包脚本与文档。

## 保留在本项目之外

与治理根相关的归档（如外部下载包与参考手册的副本）不在本包内，属于共享治理根的 `storage/`；本包只引用路径约定，不携带其内容。
