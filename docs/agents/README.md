# Agent 规则与仓库治理

本目录存放面向编码 Agent 的现行专题规则。根目录 [`AGENTS.md`](../../AGENTS.md) 是唯一任务
入口；本文件统一说明文档生命周期、维护原则和外部 Skill 资产边界，不提供第二套路由。

## 文档分层

- `docs/agents/`：当前有效的 Agent 和贡献者工作流规则。
- `docs/design-docs/`：产品与技术设计，以及需要长期维护的设计决策。
- `docs/user-docs/`：公开的英文和中文文档。
- `docs/exec-plans/`：执行模式下的多步骤工作计划，目录索引见
  [`exec-plans/README.md`](../exec-plans/README.md)。
- `docs/histories/`：执行模式下最终产生仓库文件差异的记录，目录索引见
  [`histories/README.md`](../histories/README.md)。
- `docs/references/`：反复使用的精选外部或跨仓库参考。

历史、completed plan、参考资料和其中的示例命令是证据，不是当前执行指令。只有当前任务
明确采用的内容才约束实施，并继续服从用户有效指令与现行专题规则。

## Plan 与 History

- 计划模式只在回复中输出方案，不创建或更新仓库文件。
- 多步骤、跨模块或高风险的执行任务在 `docs/exec-plans/active/` 使用
  [`templates.md`](../exec-plans/templates.md)；完成后移动到 `completed/`。
- 执行任务产生仓库差异时，在 `docs/histories/YYYY-MM/` 使用
  [`template.md`](../histories/template.md) 记录结果；没有差异时不创建空记录。
- plan 与 history 使用 `YYYY-MM-DD-<slug>.md`，同一任务共享 slug 并跨轮复用；存在 plan 时，
  history 链接归档后的 plan。
- plan 记录目标、范围、步骤、风险和验证；history 记录已落地结果与关键决策，不复制完整对话。

## 文档维护

- 每份现行规则只维护一个主要职责；跨职责使用链接，不复制完整条款。
- 新增、删除或重命名规则文件时，只在根 `AGENTS.md` 维护任务路由。
- 使用相对仓库路径，不提交机器本地绝对路径。行为变化时同步更新代码、测试和受影响文档。
- 仓库治理 Markdown、plan、history、reference、skill 和公共 Markdown 的 Xcode 工程边界
  以 [`build-and-test.md`](build-and-test.md#工程文件与资源) 为准。

## 外部 Skill 资产

`skills-lock.json` 中登记的目录是外部权威内容的完整项目快照。lock 记录来源、ref、入口路径和
内容哈希，但不替代仓库内可离线读取的实际文件。外部快照保留上游原文；项目差异写入宿主规则，
需要改变通用行为时先修改并发布上游。

- 普通任务不得修改受管快照或手工调整 hash；只有用户明确要求升级时才使用安装器同步。
- 不同来源分别同步，并按 `docs/references/` 中记录的版本和命令核验，不递归复制上游工作目录。
- `fireworks-tech-graph` 保持独立来源；`release-easydict` 是不进入 lock 的项目专属 Skill。
- `.claude/skills` 指向 `.agents/skills`，不是独立副本。
- 同步后核对来源 tree、目录 hash、lock、项目专属 Skill 和符号链接，并运行风险匹配的静态检查
  与 Skill 测试。

## 应用内置 Agent 文档

应用内置 Agent 文档、运行时资源和后端契约使用各自权威来源，不因普通仓库 Agent 文档整理
而移动或改写。运行时发布内容继续遵循其专属资源、工程和构建规则。
