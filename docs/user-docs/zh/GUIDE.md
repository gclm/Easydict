# Easydict 完整使用指南

Easydict 是一款 macOS 词典和翻译应用，支持输入翻译、鼠标划词、快捷键划词、OCR、朗读、
本地词典和多个在线/AI 服务。

## 功能概览

- 自动识别输入语言，并提供 52 种可选翻译语言；实际可用范围因服务而异。
- 输入、鼠标划词、快捷键划词、截图翻译和静默截图 OCR。
- Apple Vision OCR，并可选用有道 OCR 作为失败回退。
- Apple、百度、Bing、Google 和有道 TTS。
- 20+ 词典、翻译、AI、本地模型和 CLI 服务，完整清单见[服务总览](./SERVICES.md)。
- 主窗口、悬浮窗口和迷你窗口可分别选择服务。
- 查询历史、收藏、导出和清理；AI 结果支持 Markdown 显示。

## 安装

最新版本支持 macOS 13.0 及以上。macOS 11/12 用户可以使用旧版
[2.7.2](https://github.com/tisfeng/Easydict/releases/tag/2.7.2)，但该版本不再包含最新功能。

### Homebrew 安装（推荐）

```bash
brew install --cask easydict
```

### 手动安装

从 [GitHub Releases](https://github.com/tisfeng/Easydict/releases) 下载最新版本。

### 开发者构建

当前源码需要 macOS 13+、Xcode 16+ 和 CocoaPods。

1. 克隆仓库并切换到 `dev` 分支。
2. 在仓库目录运行 `pod install`。
3. 使用 Xcode 打开 `Easydict.xcworkspace`，不要打开 `Easydict.xcodeproj`。
4. 选择 Easydict scheme，按 `Command + R` 构建运行。

经常调试取词或 OCR 时，建议使用自己的 Apple Development 证书，避免 ad-hoc 签名导致
macOS 在重新构建后重置权限。项目脚本可以生成被 Git 忽略的本地签名配置：

```bash
chmod +x scripts/setup-team.sh
./scripts/setup-team.sh
```

无法自动检测 Team ID 时，可运行 `./scripts/setup-team.sh ABC123DE45`。没有开发者证书时可用
`./scripts/setup-team.sh --adhoc`；移除本地配置可用 `./scripts/setup-team.sh --uninstall`。

## 基本使用

| 操作 | 默认快捷键 | 结果 |
| --- | --- | --- |
| 输入翻译 | `Option + A` | 打开输入窗口，输入文本后按 Return 查询。 |
| 鼠标划词 | 无 | 选中文本后显示查询图标，悬停或点击后查询。 |
| 快捷键划词 | `Option + D` | 查询当前选中的文本。 |
| 截图翻译 | `Option + S` | 截取区域，识别文字后翻译。 |
| 静默截图 OCR | `Option + Shift + S` | 截取区域并把识别文字复制到剪贴板。 |
| 显示迷你窗口 | `Option + F` | 打开迷你查询窗口。 |

还可以在“设置 → 快捷键”中为剪贴板翻译、截图 OCR、剪贴板 OCR、显示 OCR 窗口、翻译并
替换、润色并替换等操作设置全局快捷键。这些操作默认可能没有快捷键。

## 权限

macOS 会根据使用方式请求权限：

- **辅助功能**：读取其他应用中选中的文本，以及执行替换等操作。
- **屏幕录制**：截图翻译、截图 OCR。
- **自动化**：控制浏览器、快捷指令或其他应用时使用。

在“系统设置 → 隐私与安全性”中授权。如果更换签名、移动 App 或重新构建，macOS 可能把它
视为新应用，需要重新授权。

## 划词与输入

Easydict 会根据目标应用选择合适的取词方式。若某个应用无法读取选中文本：

1. 检查辅助功能权限。
2. 尝试用 `Command + C` 确认文本本身可以复制。
3. 改用输入窗口或剪贴板翻译。
4. 对图片、扫描 PDF 或不可选择内容使用 OCR。

可在通用设置中启用输入时自动查询、反向翻译等行为。自动识别不准确时，请手动选择源语言。

## OCR

Easydict 默认使用 Apple Vision OCR；如果启用有道 OCR 回退，系统识别失败时会尝试有道。
可用语言取决于 macOS 版本，较新的系统通常提供更多识别语言。

- **截图翻译**：OCR 后立即查询已启用的服务。
- **静默截图 OCR**：只识别并复制文字，不显示翻译结果。
- **截图/剪贴板 OCR 与 OCR 窗口**：可从菜单使用，或自行设置全局快捷键。

OCR 结果不理想时，缩小截图范围、提高文字与背景对比度，并在设置中选择正确的识别语言。

## TTS 朗读

Easydict 支持 Apple、百度、Bing、Google 和有道 TTS，默认使用有道。可以在 TTS 设置中调整
服务和自动朗读行为，也可以关闭“英语单词优先使用有道”等偏好。

在线 TTS 受网络和上游接口影响；系统 TTS 的声音和语言由 macOS 已安装语音决定。

## 服务设置

新安装默认启用有道词典、DeepL 和内置 AI。打开“设置 → 服务”可以：

- 添加、移除、启用、停用和排序服务；
- 查看服务是无需密钥、项目内置、用户密钥还是 CLI 类型；
- 为需要凭据的服务填写 API Key、App ID 或 Secret；
- 为主窗口、悬浮窗口和迷你窗口分别选择服务；
- 添加多个自定义 OpenAI 兼容服务。

服务清单、访问条件和配置建议见[服务总览](./SERVICES.md)。专题配置：

- [Apple Dictionary](./How-to-use-macOS-system-dictionary-in-Easydict.md)
- [MDict](./How-to-use-MDict-in-Easydict.md)
- [Apple 翻译](./How-to-use-macOS-system-translation-in-Easydict.md)

## 查询记录与结果

- 查询历史会记录近期内容，可重新查询、收藏、导出或清理。
- 收藏适合保存需要长期复习或引用的词条。
- AI 服务返回的 Markdown 会按富文本显示；复制时仍可获取文本内容。
- 服务卡片可以重试、复制或折叠，实际操作取决于当前窗口和服务状态。

## 应用内快捷键

这些快捷键只在 Easydict 窗口位于前台时生效：

| 快捷键 | 操作 |
| --- | --- |
| `Return` / `Shift + Return` | 查询 / 输入换行。 |
| `Command + K` | 清空输入。 |
| `Command + Shift + K` | 清空输入和结果。 |
| `Command + Shift + C` | 复制查询文本。 |
| `Command + Shift + J` | 复制第一个查询结果。 |
| `Command + I` | 聚焦输入框。 |
| `Command + S` | 朗读查询文本。 |
| `Command + R` | 重新查询。 |
| `Command + T` | 交换源语言和目标语言。 |
| `Command + P` | 固定或取消固定窗口。 |
| `Command + Y` | 隐藏窗口。 |
| `Command + 小键盘 +` / `Command + 小键盘 -` | 放大 / 缩小结果字号。 |
| `Command + Return` | 使用 Google 搜索输入文本。 |
| `Command + Shift + Return` | 使用欧路词典查询输入文本。 |
| `Command + Shift + D` | 使用 Apple Dictionary 查询输入文本。 |

全局快捷键可在“设置 → 快捷键”中修改。若组合键没有响应，检查是否与其他应用或系统快捷键
冲突。

## URL Scheme

使用下面的 URL 可以从其他应用发起查询，其中 `text` 必须进行 URL 编码：

```text
easydict://query?text=hello%20world
```

旧式 `easydict://文本` 形式在部分场景中可能失败，建议始终使用完整的 `query?text=` 格式。

### 配合 PopClip 使用

安装 [PopClip](https://www.popclip.app/) 后，可将下面的 AppleScript 动作安装为扩展：

```applescript
-- #popclip
-- name: Easydict
-- icon: iconify:ri:translate
-- language: applescript
tell application "Easydict"
  launch
  open location "easydict://query?text={popclip text}"
end tell
```

## 故障排查

- **划词无效**：检查辅助功能权限，并确认目标应用允许选择或复制文本。
- **截图无效**：检查屏幕录制权限，授权后重新启动 Easydict。
- **只有某个服务失败**：检查该服务是否启用，以及凭据、CLI 登录、本地地址和网络状态。
- **语言不受支持**：切换服务；不同服务、OCR 和 TTS 的语言覆盖并不相同。
- **设置没有生效**：退出并重新打开 Easydict，再检查是否运行了多个版本。

## 参与贡献

- 开发流程和代码贡献见[贡献指南](../../../CONTRIBUTING.md)。
- 本地化贡献见[如何翻译 Easydict](./How-to-translate-Easydict.md)。
- 问题和建议请提交到 [GitHub Issues](https://github.com/tisfeng/Easydict/issues)。
