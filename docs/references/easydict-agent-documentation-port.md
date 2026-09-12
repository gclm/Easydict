# Easydict Agent 文档治理移植参考

## 来源

本参考对应 Scoco `dev` 上连续的五个 Agent 文档治理提交：

- `85d67f2da`：简化 Agent 文档入口与治理。
- `8d46489f5`：记录 Agent 文档设计和外部参考。
- `7ef43b892`：拆分外部参考目录与专题内容。
- `927793cc9`：强制记录仓库差异并补充文档结构。
- `fb57ab64e`：简化 Agent 规则职责。

## 采用范围

- 采用唯一 Agent 入口、职责分层、计划/执行模式和 plan/history 生命周期。
- 采用 design docs 与 references 的分层，用于记录结构理由和来源证据。
- 采用“执行任务产生仓库文件差异时保留同任务 history”的记录约定。

## Easydict 本地差异

- 保留 Easydict 的默认 PR base、`release-easydict`、Swift/Xcode 和 String Catalog 规则；
  通用工作流细节由对应 Skill 自身维护。
- 不引入 Scoco 的 release、R2/OCU、boss-resume、贡献者文档或产品专属规则。
- 本文件只记录来源与本地取舍，不替代 `AGENTS.md` 或 `docs/agents/` 中的现行规则。

## 重新评估条件

- Scoco 改变 Agent 文档入口、职责分层、任务模式或 history 约定。
- Easydict 的 Agent 运行时、Xcode 工程或本地交付规则发生结构性变化。
- 本参考中的提交无法在来源仓库中核对，或本地采用点已经过期。
