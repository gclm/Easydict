# AGENTS.md

Easydict 是一款 macOS 词典和翻译应用，支持查词、文本翻译、划词翻译和 OCR
截图翻译。

`AGENTS.md` 是 Agent 的唯一任务入口；详细规则只在对应专题文档维护。

## 始终阅读

- 每个任务先按 `docs/agents/task-modes.md` 判断计划模式或执行模式。
- 回复和内部任务记录使用用户当前请求的语言；已有文档保持原语言，公共文档遵循 `en/zh`
  目录，用户明确要求翻译时除外。代码标识、API 名称、命令、路径、品牌名称和固定输出契约
  保留原文。
- 再按当前任务读取下方最小必要规则；同一任务中内容未变化的规则和证据可以复用。

## 任务路由

- 构建、测试、工程文件与资源、Xcode 验证：`docs/agents/build-and-test.md`。
- 跨语言代码质量、Swift、Objective-C、SwiftUI、API 和本地化：
  `docs/agents/coding-guidelines.md`。
- 文档分层、计划、history、参考资料、外部 Skills 和同步边界：
  `docs/agents/README.md`。
- 产品代码、跨功能行为或模块边界：`docs/design-docs/application-architecture.md`。
- 公共使用或贡献者文档：`docs/user-docs/en/` 或 `docs/user-docs/zh/`。

## 项目默认值

- GitHub Pull Request 默认合入 `dev`。
