# 自动化

DSH 的定时能力来自宿主级调度工具：`schedule_create` / `schedule_list` / `schedule_update` / `schedule_delete`。任务持久化在宿主，重启后仍有效。

## 参数模型

- `delivery`（必填）：`this-session` 复用发起会话的资源；`new-session` 起独立运行，有自己的工作区、权限与模型。
- 时间选择器六选一：`after_seconds`、`at`、`every_seconds`（≥60）、`daily{time,time_zone}`、`weekly{time,time_zone,weekdays}`、`cron{expression}`。
- 可选：`permission`（read-only / workspace-write / danger-full-access）、`workspaceId`、`model`、`provider`。
- `this-session` 不能覆盖资源；改期或改指令用 `schedule_update`，保留 id 与记录。

巡检类任务一律用 `read-only`，只读诊断不写盘；整理类任务按实际需要给 `workspace-write`。

## 每日只读巡检模板

```
定时：daily 09:00（Asia/Shanghai）
delivery：this-session
permission：read-only
prompt：
Run a read-only DSH workspace inspection for root "$HOME/Desktop/OH-WorkSpace":
1. Use the project roots supplied by this session; never guess them by scanning the disk.
2. Run python "$HOME/.dsh/skills/dsh-optimizer/scripts/dsh_optimizer.py" diagnose \
     --root "$HOME/Desktop/OH-WorkSpace" --dsh-home "$HOME/.dsh" --json
3. Summarize findings in at most 30 lines: counts, largest items, risks, and anything that changed since yesterday.
4. Do not modify, move, or delete anything. Do not print credentials, tokens, or the contents of .credentials.yaml.
```

## 每周整理模板

```
定时：weekly 周六 10:00（Asia/Shanghai）
delivery：this-session
permission：workspace-write
prompt：
Run a weekly DSH workspace organization pass for root "$HOME/Desktop/OH-WorkSpace":
1. Use the project roots supplied by this session; list them explicitly when passing --project-root.
2. Run organize-scan, then group candidates into safe-to-relocate, needs-isolation, and report-only.
3. Present the plan and wait for confirmation before applying anything.
4. Apply only low-risk items; anything touching credentials, databases, sessions, or unique sources is report-only.
5. Write one record per applied batch and report the rollback path.
```

## 约束

- 只用绝对路径，但让 runtime 在每次运行时重新核对根与项目根。
- 任务里不要打印 `.credentials.yaml`、`.env`、token 或会话内容。
- 巡检任务不得调用 `apply`、`rollback`、`purge` 的写路径。
- 失败处理：同一类失败最多主动修正一次；同类失败再现就报告卡点与已得到的结果，不循环重试。

## 展示而不自动创建

skill 不自动创建定时任务。用户要自动化时，把上面的模板与参数模型展示出来，由用户确认后再调 `schedule_create`。创建后可以用 `schedule_list` 核对，用 `schedule_update` 改期或暂停。
