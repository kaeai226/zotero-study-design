# Zotero 研究设计比较助手

版本：0.1.0。中文指令型 skill，适合围绕已确定的研究问题，比较选定论文的研究设计，并形成适合自身条件的方案草案。

支持实验、观察／调查、质性及混合方法。第一版以设计研究与人机交互研究为主要使用范围，其他学科需要结合领域知识复核。

## 现在能做什么

- 按论文及子研究提取对象、取样、材料、流程、测量、分析与局限，保留证据定位。
- 围绕用户问题、现实条件及目标主张比较方法适用性。
- 区分来源事实、比较推断和新方案建议，记录未报告或未取得的信息。
- 形成自有方案草案和人工核验记录。

这是由 AI 助手执行的指令包，不是 Zotero 原生插件。Zotero 用于选择、整理和导出文献；本包不包含自动连接 Zotero、读取账户、调用模型的程序或一键写回功能。

## 运行条件

使用能够读取本机／上传文件的 AI 助手。推荐在支持本地 skills 的 Codex 中运行；已有文件阅读工具即可使用这套指令，不需要为本包单独申请 API 密钥。

宿主需要能读取论文内容。扫描、乱码或关键图表需要相应的视觉／识别能力；不具备时，助手应标明读取限制。没有文件写入能力时，只能在对话中交付五个对应部分，不能声称已经保存结果。

## 快速开始：无需安装的显式读取

1. 解压并保留完整 `zotero-study-design` 文件夹，包括 `references` 和 `templates`。
2. 在 Zotero 中选择本次要比较的文献，导出条目信息，并提供对应的可读 PDF 全文和需要的补充材料。只有元数据或摘要时也可以开始，但只能分析实际取得的内容。参见 [Zotero 导出说明](https://www.zotero.org/support/kb/exporting)。
3. 在自己的研究工作区新建 `inputs`，放入资料；复制并填写 [研究说明模板](templates/research-brief.md)。研究资料与运行输出不要放进待公开的 skill 源码。
4. 将下面的指令发给能访问这些文件的 AI 助手，替换路径为实际位置：

```text
请先读取 <skill目录>/SKILL.md，并按其中工作流执行。
研究说明：./inputs/research-brief.md
文献与补充材料：./inputs/
输出目录：./outputs/run-01/
请提取逐项研究的方法证据，比较它们对我的研究问题的适用性，
形成有来源的自有方案草案和人工核验记录。
```

相对路径以你与助手约定的研究工作目录为准。本机文件路径不会使普通网页聊天自动获得本机访问权；在没有本机文件工具的环境，需要通过该环境支持的上传功能提供材料。

## 可选：安装为 Codex 可发现的 skill

把整个 `zotero-study-design` 文件夹复制到以下位置之一：

- 用户范围：`~/.agents/skills/zotero-study-design/`。Windows 可在文件资源管理器进入 `%USERPROFILE%\.agents\skills` 后复制。
- 项目范围：`<项目目录>/.agents/skills/zotero-study-design/`。

如已有同名版本，先检查并保留旧版本，再决定是否替换。安装后从可用的技能选择器选择本 skill；支持 `$` 提及的 Codex 界面也可输入：

```text
$zotero-study-design
请读取我的研究说明和选定文献，比较研究设计并生成方案草案。
```

Codex 会检测 skill 变化；若没有出现，可重启后检查。仅把文件夹放到普通 `output` 目录不等于完成上述安装。上述目录与发现方式依据 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

## 默认交付

| 文件 | 内容 |
|---|---|
| `01-source-register.md` | 当前问题、条件、材料与实际阅读状态 |
| `02-design-evidence.md` | 每项研究的方法事实、样本口径及原文定位 |
| `03-design-comparison.md` | 适用性、迁移条件、实施代价及证据缺口 |
| `04-proposed-design.md` | 有条件的方案草案、修订依据或暂不能选择的原因 |
| `05-review-and-run-log.md` | 核验状态、错误修正、实际运行条件与用户指令 |

默认输出 Markdown；用户指定格式优先。模型会有波动，可复现目标是输入、步骤和依据可回查，而非每次输出逐字相同。

## 分步使用与核验

完整运行后，可以继续要求：

```text
请只检查第二份文件中影响最终推荐的事实，逐条回到原文。
标出没有原文定位、仅据摘要或包含推断的内容。
```

```text
我已经人工核对以下项目：[列出项目与真实核验记录]。
请更新核验状态，并据此修订方案；其他项目保留待人工复核。
```

```text
我现在的资源条件变为：[填写变化]。
请复用已经核验的方法证据，更新适用性比较和方案，并记录这次修改。
```

助手的原文回查不等于人类已经确认。生成的研究方案也不等于方案效果已经被实验验证。

## 案例

[家庭群聊案例](examples/family-chat.md) 展示如何把真实研究问题填入通用流程。本包只提供研究说明和操作提示，不附私人聊天、课程作业或论文全文。

## 验证范围

截至 2026-10-26，已完成七份文件的内部链接、名称、描述与界面字段检查，以及两组独立行为试运行：

- 家庭群聊：实际读取两篇论文全文与一份方案草案，生成五份输出，保留样本关系、研究目的、情境迁移与人工核验边界。
- 办公空间：使用明确标注的合成材料，生成五份输出，检查多项研究分开提取、摘要缺证保留、重复记录与独立样本区分。合成材料不提供真实研究效果证据。

两组均通过显式路径读取本 skill；这不等于已经完成宿主自动发现测试。试运行只检查工作流行为，不证明推荐方案具有现实效果，也不保证换模型后逐字复现。

标准 `quick_validate.py` 在当前环境因缺少 PyYAML 未能运行，现有结构检查和 YAML 静态审查不等于完整解析器验证。论文细节、方法适配和实施条件仍需研究者复核。

尚未实测 Zotero 自动连接／写回、Codex 自动发现、跨宿主兼容及 GitHub 网页上传；这些功能不属于已经验证的能力。

## 上传到 GitHub

1. 在 [GitHub 新建仓库](https://github.com/new)，建议仓库名 `zotero-study-design`，选择你的账号及需要的公开／私有可见性。这里已有 README，不必额外生成另一份。
2. 创建后进入仓库，选择 **Add file → Upload files**；空仓库也可能先显示上传现有文件的入口。
3. 上传解压后本文件夹内的文件及子目录。检查 `README.md` 和 `SKILL.md` 位于仓库根目录，`templates`、`references`、`examples`、`agents` 保持结构；不要只上传 ZIP。
4. 填写提交说明，例如 `Add research design comparison skill v0.1.0`，按页面提交。已有仓库如需要分支或拉取请求，按其规则操作。
5. 打开仓库 README 检查图片／链接与文件结构；其他人可下载该文件夹并按前面的方式使用。

只上传本 skill 源码目录，不上传它外层的项目开发方案、试运行、私人资料或本机启动指令。`.gitignore` 为使用 Git 时提供的辅助规则，网页手动上传仍需自己选择文件。

官方步骤：[创建仓库](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)、[上传现有文件](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)。发布到 GitHub 与在插件目录发布是不同流程；本包提供的是可下载的 skill 源文件。

## 目录

```text
zotero-study-design/
├── SKILL.md
├── README.md
├── .gitignore
├── agents/openai.yaml
├── references/output-format.md
├── templates/research-brief.md
└── examples/family-chat.md
```

## 许可状态

本版本尚未选定独立开源许可证；仓库所有者发布时可另行决定并补充 LICENSE。本包不随附论文全文或私人研究材料。
