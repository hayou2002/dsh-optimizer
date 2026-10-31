# 通道与工具

| 需求 | 首选通道 |
|---|---|
| 项目根 | 会话传入的 `--project-root` 与工作区现场 |
| 定时任务 | `schedule_create` / `schedule_list` / `schedule_update` / `schedule_delete`，`delivery` 必填 `this-session` 或 `new-session` |
| 长期知识与指令维护 | `$DSH_HOME/AGENTS.md`、`~/.agents/AGENTS.md`、项目 README（无原生记忆控制面） |
| Skills 安装、启用、停用 | `$DSH_HOME/skills`（只读审计，安装与停用走 skill 根目录） |
| MCP 与集成 | 只读审计；连接走配置与 `.plugin-backups/`，不手改集成文件 |
| 文件扫描、计划、事务 | `scripts/dsh_optimizer.py` |
| 文件内容读取 | 普通文件工具；认证和数据库只取元数据 |
| GitHub 发布 | `gh` 或已连接的 GitHub 能力 |
| 跨 Agent 共享根协作 | `.optimize/COLLABORATION.md` + `collaborate` 子命令 |

## 文件事务

- 计划生成后，用 CLI 验证和执行。
- 涉及项目根时，把项目根显式传入。
- 修改前核对路径真实化结果与 root/project 边界。
- 默认不跟随链接。
- 项目冲突以 hash 判断。

## 不可越过的通道

- 不通过手工删除插件目录实现卸载。
- 不直接改 DSH 会话数据库或 SQLite 状态。
- 不把认证 token 输出到对话、日志或报告。
- 不用 shell 字符串拼接执行用户路径；参数以独立 argv 传递。
- 不用 `git reset --hard`、强制 push 或强删回收区绕过事务。

## 交互

- 失败后先说明未完成范围，再恢复本批次。
- 用户只想查看时保持 diagnose 零写入。
- 高风险动作展示计划摘要；低风险动作在执行后仍报告批次。

