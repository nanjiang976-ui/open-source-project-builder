<a id="title"></a>

# 项目开源助手｜标题与简介 · Title and Description

在支持 Agent Skills 的 Agent 里打开你的项目，说一句“带我逐步开源”。助手先查看文件，再和你确定谁会用它、那个人第一次要完成什么。等你选好本轮的范围，它再帮你整理 README、示例或发布清单。

**适合第一次把自用项目交给别人使用的作者。** 手上有一个普通文件夹就能开始。README 是访客打开仓库时先看到的说明；Skill 是可以安装给 Agent、在不同项目里反复使用的一套工作指引。

[如何安装](#install) · [第一次怎么问](#first-run) · [看一段真实对话](#guided-example) · [开源与 README 原文](#sources) · [34 个模块目录](#modules)

<a id="features"></a>

## 功能与使用场景 · Features

| 你现在需要什么 | 助手会怎么做 |
|---|---|
| 带我第一次开源这个工具 | 核对现有材料，每轮提出影响后续工作的选择，解释原因并给出建议。你确认读者、首次任务和本轮材料后，助手再开始写。 |
| 只检查别人会卡在哪里 | 沿着 README 的步骤找实际文件、入口和输出，直接告诉你已有材料、首要卡点及验证办法。 |
| 只补 README 的一个段落 | 按你指定的范围写入或给草稿，保留已有内容。 |
| 尚无仓库，只有一个开源想法 | 从目标读者的实际问题开始，收敛到能演示价值的首版和下一个可验证动作。 |

它检查的重点随项目而变。命令行工具看首条命令和输出，桌面应用看安装包和首次操作，开发库看最小调用和返回值，自部署应用看配置、启动与访问，Skill 看什么时候调用以及怎么认出结果。

<a id="install"></a>

## 如何安装 · Installation

三种方法选一种。你需要一个支持本地 Agent Skills、能打开项目并读取文件的 Agent。下面是**当前用户级安装**，装好后可以在这台机器上的多个项目里使用。已有同名 Skill 时，先看[常见问题](#faq)。

| Agent | macOS／Linux 的个人技能目录 | Windows 的个人技能目录 | 在项目对话中点名 |
|---|---|---|---|
| Codex | `~/.agents/skills/` | `%USERPROFILE%\.agents\skills\` | `$open-source-project-builder` |
| Claude Code | `~/.claude/skills/` | `%USERPROFILE%\.claude\skills\` | `/open-source-project-builder` |

其他兼容 Agent 可在安装器里选相应名称，或按该客户端文档找到个人技能目录及调用方式。[安装器支持的 Agent](https://github.com/vercel-labs/skills/blob/main/docs/agents.md) · [Codex 技能目录](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) · [Claude Code Skills](https://code.claude.com/docs/en/skills)

### 方法一：用 npx 安装（推荐）

在终端运行下面的命令，按提示选择你使用的 Agent。`-g` 表示安装到个人范围，`--skill` 指定这个仓库里的“项目开源助手”。本次核对的 Skills CLI 1.9.0 需要 Node.js 22.20.0 或更高版本，可用 `node --version` 检查。没有 Node.js 时可直接选方法二或三。[CLI 命令](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) · [1.9.0 的运行环境声明](https://github.com/vercel-labs/skills/blob/57217cf86ba38148a57af9e90d14a4c049558330/package.json)

```sh
npx skills add nanjiang976-ui/open-source-project-builder --skill open-source-project-builder -g
```

### 方法二：用 Git 克隆后复制 Skill

需要 Git。在普通工作目录里运行下面的命令，选择尚无同名子目录的位置。克隆成功后，留在刚才运行命令的目录。仓库里的 `skills/open-source-project-builder/` 才是要安装的那一层。

```sh
git clone https://github.com/nanjiang976-ui/open-source-project-builder.git
```

**Windows PowerShell**。下面的目标以 Codex 为例；使用 Claude Code 时，把 `'.agents/skills'` 改为 `'.claude/skills'` 再执行。

```powershell
$sourceDir = (Resolve-Path -LiteralPath './open-source-project-builder/skills/open-source-project-builder' -ErrorAction Stop).Path
$skillsDir = Join-Path $env:USERPROFILE '.agents/skills'
$destination = Join-Path $skillsDir 'open-source-project-builder'

if (Test-Path -LiteralPath $destination) {
    Write-Output '目标已存在，请先查看已有版本。'
} else {
    New-Item -ItemType Directory -Path $skillsDir -Force -ErrorAction Stop | Out-Null
    Copy-Item -LiteralPath $sourceDir -Destination $destination -Recurse -ErrorAction Stop
    Get-Item -LiteralPath (Join-Path $destination 'SKILL.md')
}
```

**macOS／Linux 终端**。下面同样以 Codex 为例；使用 Claude Code 时，把 `"$HOME/.agents/skills"` 改为 `"$HOME/.claude/skills"`。

```sh
source_dir="./open-source-project-builder/skills/open-source-project-builder"
skills_dir="$HOME/.agents/skills"
destination="$skills_dir/open-source-project-builder"

if [ -e "$destination" ] || [ -L "$destination" ]; then
    printf '%s\n' '目标已存在，请先查看已有版本。'
elif [ -f "$source_dir/SKILL.md" ]; then
    mkdir -p "$skills_dir" && cp -R "$source_dir" "$destination" && ls "$destination/SKILL.md"
else
    printf '%s\n' '请回到刚才执行 git clone 的目录。'
fi
```

### 方法三：下载 ZIP 手动安装

1. [下载主分支 ZIP](https://github.com/nanjiang976-ui/open-source-project-builder/archive/refs/heads/main.zip) 并完整解压，打开包含本篇 README 的目录。
2. 打开 `skills`，复制里面的 **`open-source-project-builder` 文件夹**。打开它应能直接看到 `SKILL.md`、`agents/`、`references/`、`LICENSE` 和 `THIRD-PARTY-NOTICES.md`。
3. 在文件管理器中打开上表里所选 Agent 的个人技能目录。目录尚不存在时，先创建它，再粘贴。Windows 的 `%USERPROFILE%` 和 macOS／Linux 的 `~` 都指当前用户的个人目录。此方法无需安装 Git 或 Node.js。
4. 核对安装后的目录结尾是 `skills/open-source-project-builder/SKILL.md`。打开目标项目的新对话，按下一节实际调用。如果 Agent 尚未刷新技能列表，重新打开客户端再试。

<a id="first-run"></a>

## 首次使用与示例 · Usage/Examples

**先打开你想开源的项目。** 在项目对话中用上表的名字点名 Skill，再接下面任一段话。

**带我走一遍完整流程**

```text
带我逐步开源当前项目。先看看已有材料，问我现在最值得决定的问题。
```

助手会给出一项从文件中看到的事实、一组当前需要决定的问题和推荐。你可以答“同意”，也可以告诉它你要服务另一类读者。下一轮应该顺着你的选择继续。

**先给我一次只读体检**

```text
只读检查这个项目。告诉我新用户最早会在哪一步卡住，给出文件依据和最值得先补的一项，等我选定范围再整理。
```

打开它点名的文件，检查是否真的缺了入口或示例。若你早已知道要改什么，可以直接说“只补 README 的安装一节，写清楚要复制哪层目录、安装后怎样验证”。

<a id="guided-example"></a>

## 两条实际对话路径 · Demo

我们用同时提供 HTML 成品和源码的 WordCounter 字符统计工具测试了两条路径。两次真实 Codex 会话，都从作者请助手“带我逐步开源这个项目”开始。助手核对文件后，请作者先决定首页优先服务谁。

| 作者的回答（原话） | 第二轮的实际回复（摘录） | 讨论进入了哪一步 |
|---|---|---|
| 首版面向普通用户，优先让他们直接用上成品。 | “第二步，确认成品入口和第一次使用的成功标志。” | 从哪里拿到 HTML，打开后输入 `你好ABC`，点击「统计」是否应得到 `5`。这是该轮提出的预期结果。 |
| 首版面向开发者，优先让他们从源码入手。 | “第二轮确认开发者拿到源码后，第一次做到哪一步算成功？” | 是先运行 `npm test` 验证逻辑，还是接着 `npm run build`，打开生成的页面。 |

<a id="example"></a>

只读体检也可以得到一个很小但具体的结论。例如助手检查自己的旧版时，找到了给 Agent 读的执行说明，却没有找到教初次使用者安装和第一次调用的首页。作者据此补齐了首次使用路径。[助手自身的前后对照](docs/cases/self-review.md) · [WordCounter 的测试记录](docs/cases/guided-review.md)

<a id="local-run"></a>

## 在自己的项目里运行 · Run Locally

安装后，打开一个你熟悉的普通项目目录，检查当前对话的工作目录是否正确，点名 Skill 并发出只读请求。成功标志是 Agent 能说出项目里某个**真实存在的文件**、读者会在哪一步遇到困难，以及怎样验证补齐后的效果。本 Skill 由 Agent 加载文本说明，无需启动单独服务。

<a id="verification"></a>

## 怎样验证 · Running Tests

| 你想验证什么 | 可以怎样复查 |
|---|---|
| 分轮引导是否有效 | 用同时有成品和源码的项目开两个新对话，分别选“普通用户”和“开发者”，观察第二轮是否分别追问成品入口和构建路径。 |
| 只读体检是否守住范围 | 在项目副本上保留修改前的记录，发出“只读检查”请求，再比对文件内容。 |
| 单项修改是否准确 | 指定只补 README 的某一节，实际执行补充的命令，并对照目标段落以外的文件和文字。 |

既有 Windows Codex 桌面后端的记录覆盖技能发现、多轮回复以及两种快捷请求的实际改动范围。记录中分别标明实际运行、根据源码推导的预期，以及仍待真人操作的环节。[分轮引导与快捷入口实测](docs/cases/guided-review.md) · [首次安装与调用](docs/cases/self-review.md)

2026 年 11 月 19 日，我们还把[公开版本的 Skill](https://github.com/nanjiang976-ui/open-source-project-builder/tree/80f89a37307f4d674bda0bd8604126096268089b/skills/open-source-project-builder) 安装到了以下两个客户端的个人目录。在每个客户端中，都打开了一个没有项目级 Skill 的普通项目，实际进行了两轮对话。

| 实测环境 | 两轮对话中观察到什么 |
|---|---|
| Windows · Codex 桌面后端 | 仅发现一个同名的用户级 Skill。助手识别出 ClipClock 的 HTML 成品和源码，作者选开发者后，第二轮转向测试、构建和成功标志。独立运行测试与构建均通过。 |
| Windows · Claude Code 2.1.150 | 在 InkCount 项目里用 `/open-source-project-builder` 点名后，助手读到了离线 HTML 和 Python 入口。作者选普通读者后，第二轮讨论怎样取得并打开 HTML、首次操作怎样验收。 |

两个样例的文件内容在引导前后一致。Claude Code 首轮曾把 InkCount 的命令行输入描述为管道；请它核对入口后，它更正为文件路径参数。独立运行 `python inkcount.py examples/morning.txt` 得到 `3`。验证自己的项目时，也可以请 Agent 指出命令依据，再亲自核对输出。macOS 和 Linux 给出了对应的安装命令，干净系统上的首次调用以及真人独立上手列在[后续方向](#roadmap)。

<a id="faq"></a>

## 常见问题 · FAQ

**项目还没有放上 GitHub，可以用吗？** 可以。Agent 直接检查本地目录；发布包、远程设置或在线链接等看不到的内容会标为待确认。

**我已有 README，怎样先看问题？** 在请求中写“只读检查”，或写“先给草稿”。准备修改时，可以指定文件和段落。

**安装后没有识别，或看到旧版行为，怎么排查？** 先检查当前 Agent 的个人技能目录和正在打开的项目目录里有没有同名 Skill，再打开内层 `SKILL.md`，看其中是否有“分轮引导”。旧版本也可能使用相同显示名。备份旧版时，放到 Agent 不会扫描的其他目录。回到目标项目，在新对话中显式点名测试。

**助手会替我选许可证或自动发布吗？** 你决定项目和第三方材料的授权范围。准备发布清单、实际推送和公开发行是不同的操作，执行范围以你的具体请求为准。

<a id="docs"></a>

## 详细文档 · Documentation

- 想看不同项目为何要用不同的 README 顺序，可以从中文研究报告开始。[十个高星仓库的结构与写法](docs/research.md)
- 想知道助手如何根据项目类型检查入口、示例与首次成功标志，可以读随包参考。[项目类型与发布检查](skills/open-source-project-builder/references/repo-blueprints.md)
- 想复核它会不会为已有材料重复提建议，可以看对一个已有中英文教程和许可的项目所做的只读检查。[迁移助手检查记录](docs/cases/migration-review.md)

<a id="sources"></a>

## 开源与 README 原文 · Related

| 我想弄清什么 | 适合读的原文 |
|---|---|
| 第一次公开项目，还应准备哪些事？ | 从开源目标、许可证和贡献方式读到发布前检查。[GitHub 中文《开始一个开源项目》](https://opensource.guide/zh-hans/starting-a-project/) |
| 我想参考一份可以照着起草的 README。 | 查看简介、安装、使用、贡献和许可的排列，以及随附的空白模板。[Best-README-Template](https://github.com/othneildrew/Best-README-Template) |
| 我希望几个开发库采用一致的文档写法。 | 对照规范、中文说明和示例，检查安装、调用、维护者与贡献说明。[Standard Readme](https://github.com/RichardLitt/standard-readme) |

<a id="tech"></a>

## 技术与文件 · Tech

`SKILL.md` 是 Agent 读取的 Markdown 指令，元数据写在文件开头的 YAML 中。`references/` 放按需读取的项目类型参考。`agents/openai.yaml` 提供兼容客户端使用的显示名和默认提示。安装整个内层目录还能同时保留两份许可说明。[技能文件](skills/open-source-project-builder/SKILL.md) · [Agent Skills 格式规范](https://agentskills.io/specification)

<a id="environment"></a>

## 环境变量 · Environment Variables

本 Skill 没有自定义必填环境变量或专用 API 密钥。Agent 的登录和模型访问沿用你已有的配置。安装示例里的个人目录变量用于定位文件夹。

<a id="feedback"></a>

## 问题与建议 · Feedback

遇到问题时，请附上 Agent 名称和版本、操作系统、安装方式、触发请求、预期结果与实际表现。涉及私人项目时，用示例路径替换真实路径，省略密钥和聊天中的私人信息。[提交 Issue](https://github.com/nanjiang976-ui/open-source-project-builder/issues)

<a id="support"></a>

## 使用支持 · Support

安装或调用遇到困难，可以先按常见问题核对目录层级和同名 Skill，再到 Issues 搜索相同症状，或开一条新问题说明自己停在哪一步。[安装常见问题](#faq) · [GitHub Issues](https://github.com/nanjiang976-ui/open-source-project-builder/issues)

<a id="contributing"></a>

## 怎样参与 · Contributing

欢迎用 Issues 反馈问题或提出建议，也欢迎发 Pull Request 改进文档、示例和 Skill。改文档时说明哪个步骤会让读者卡住；改行为时请附一条可以复现的请求、预期结果，以及你用哪个 Agent 验证过。示例项目和截图请先移除私人内容。[Issues](https://github.com/nanjiang976-ui/open-source-project-builder/issues) · [Pull Requests](https://github.com/nanjiang976-ui/open-source-project-builder/pulls)

<a id="roadmap"></a>

## 后续方向 · Roadmap

- 在 macOS 和 Linux 的干净环境里，从公开仓库重新安装并完成首次调用，记录与 Windows 的差异。
- 请第一次开源的作者独立完成一次引导，根据他们实际停下或误解的地方改进教程。

<a id="authors"></a>

## 作者 · Authors

项目由 **Jiangnan-Studio** 维护。[GitHub · @nanjiang976-ui](https://github.com/nanjiang976-ui)

<a id="credits"></a>

## 致谢 · Acknowledgements

分轮引导的方法改编自 Matt Pocock 的 `grilling`。readme.so 为下方的模块目录提供了章节清单；参与研究的十个公开仓库提供了不同读者首次上手的实例。[grilling 固定版本](https://github.com/mattpocock/skills/blob/5863806dd4e15c63174bee4e7515a4256792ecfa/skills/productivity/grilling/SKILL.md) · [十个案例的出处](docs/research.md)

<a id="lessons"></a>

## 实践中学到什么 · Lessons

用自己的旧版做首次体检时，我们发现示例目录树里虽然写着 `README.md`，实际交给读者的文件夹里却没有这份文档。后来改用读者实际拿到的包验收，逐步核对“复制哪一层、在哪里调用、出现什么算成功”。[首次体检的文件依据](docs/cases/self-review.md)

<a id="license"></a>

## 许可证 · License

本项目采用 MIT 许可证，版权署名为 Jiangnan-Studio。改编自 `grilling` 的部分保留 Matt Pocock 的版权和 MIT 许可全文。两份声明都会随可安装的 Skill 一起分发。[项目许可证](LICENSE) · [第三方许可说明](skills/open-source-project-builder/THIRD-PARTY-NOTICES.md)

<a id="badges"></a>

## 徽章 · Badges

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

<a id="modules"></a>

## 附录：亲手拼一份 README · Appendix

你正在读的就是一份适用于 Agent Skill 的完整 README 示例。不同项目面对的读者和首次任务不同，没有一种模板适合所有项目。

**[打开 readme.so 可视化编辑器](https://readme.so/editor)**

在编辑器里选择 **Installation** 和 **Usage/Examples**，填入你自己的最短安装步骤与第一次操作，切换到 **Preview** 看效果。若项目需要独有的章节，可用 **Custom Section** 补上，例如桌面工具的“怎样导出第一份文件”。

### 34 个模块的可点击目录

每个名称都链接到本文对应的真实标题。下方也保留目前用不上的章节，方便你看到它们适用于哪种项目。

| 模块名称 | 简要说明 | 本项目的用法或取舍 |
|---|---|---|
| [标题与简介 · Title and Description](#title) | 介绍项目为谁解决什么问题。 | 从本地已有项目、准备首次开源的作者讲起。 |
| [主要功能 · Features](#features) | 说明能交给它哪些任务。 | 分轮引导、只读体检、单项整理和首版规划。 |
| [如何安装 · Installation](#install) | 准备运行环境并正确放置文件。 | 三种渠道、跨平台命令及两个客户端的个人目录。 |
| [用法与示例 · Usage/Examples](#first-run) | 展示一次可复制的输入。 | 按当前目标选择逐步引导或只读检查。 |
| [演示 · Demo](#guided-example) | 看工具怎样响应真实操作。 | 同一项目，两种读者选择，引出不同的第二轮。 |
| [运行测试 · Running Tests](#verification) | 说明怎样复现和判断成功。 | 用分支对话和文件差异核对实际行为。 |
| [常见问题 · FAQ](#faq) | 解决安装和使用时常见的疑惑。 | 核对普通文件夹、同名旧版和写入范围。 |
| [反馈 · Feedback](#feedback) | 说明报错与建议应附哪些信息。 | 从实际卡住的一步提交 Issue。 |
| [许可证 · License](#license) | 说明能怎样使用和分发。 | 项目 MIT 正文和第三方相关声明。 |

<details>
<summary>展开其他 25 个模块的说明与链接</summary>

| 模块名称 | 简要说明 | 本项目的用法或取舍 |
|---|---|---|
| [详细文档 · Documentation](#docs) | 给想深入了解的读者一个入口。 | 案例、研究报告、项目类型参考。 |
| [本地运行 · Run Locally](#local-run) | 说明第一次从哪里启动。 | 在自己的项目中让 Agent 读取并调用已安装的 Skill。 |
| [技术与文件 · Tech](#tech) | 说明实现使用的技术和材料。 | Markdown 指令、YAML 元数据与按需读取的参考。 |
| [环境变量 · Environment Variables](#environment) | 列出运行前需要配置的变量。 | 本 Skill 没有自定义必填变量。 |
| [使用支持 · Support](#support) | 让读者找到求助渠道。 | 先查 FAQ，再搜索或提交 Issue。 |
| [贡献方式 · Contributing](#contributing) | 说明欢迎怎样参与和验证。 | 接受 Issues 和文档、示例、行为改进的 PR。 |
| [路线图 · Roadmap](#roadmap) | 列出后续希望验证的方向。 | 干净环境安装与新手独立试用。 |
| [作者 · Authors](#authors) | 说明谁在维护这个项目。 | 列出作者公开署名与 GitHub 主页。 |
| [相关项目 · Related](#sources) | 给读者可直接查阅的原文。 | 按问题列出三个辅助开源的项目与指南。 |
| [致谢 · Acknowledgements](#credits) | 保留借鉴来源与归属。 | 感谢 grilling、readme.so 和提供实例的仓库。 |
| [经验总结 · Lessons](#lessons) | 记录实践中发现的问题和解法。 | 示例目录里的名字需要对照实际交付文件。 |
| [徽章 · Badges](#badges) | 展示可核实的项目状态。 | 只展示链接到许可正文的 MIT 徽章。 |
| [附录 · Appendix](#modules) | 收纳模块目录、工具和补充材料。 | 提供可视化编辑器及本模块对照表。 |
| [公共接口 · API Reference](#api) | 记录公共 API 的参数、响应和错误。 | 本 Skill 通过 Agent 对话使用，目前没有公共 API。 |
| [部署 · Deployment](#deployment) | 说明怎样部署服务或托管应用。 | 当前交付物是本地安装的指令文件。 |
| [配色参考 · Color Reference](#colors) | 展示界面主题、调色板或设计规范。 | 本项目没有独立界面或配色系统。 |
| [项目标识 · Logo](#logo) | 展示可公开使用的项目标识。 | 目前没有单独发布的项目标识。 |
| [项目截图 · Screenshots](#screens) | 用可见界面辅助读者完成操作。 | 目前用有来源的对话摘录演示，未提供项目截图。 |
| [性能优化 · Optimizations](#opts) | 记录优化措施和可复核的测试数据。 | 目前没有可公布的性能对比。 |
| [使用者 · Used By](#used) | 展示可核实且愿意公开的使用者。 | 目前没有公开的使用者名单。 |
| [个人简介 · Github Profile - Introduction](#profile-intro) | 为 GitHub 个人主页编写开场介绍。 | 适用于个人主页；此处是项目仓库。 |
| [关于我 · Github Profile - About Me](#profile-about) | 在个人主页介绍作者背景。 | 项目读者可从作者章节访问公开主页。 |
| [个人链接 · Github Profile - Links](#profile-links) | 在个人主页汇集网站和社交链接。 | 项目支持与反馈渠道另有专节。 |
| [个人技能 · Github Profile - Skills](#profile-skills) | 在个人主页展示掌握的技术。 | 项目功能已在使用场景中列出。 |
| [其他个人信息 · Github Profile - Other](#profile-other) | 在个人主页补充动态或合作意向。 | 目前没有与本项目有关的个人动态。 |

</details>

## <a id="api"></a>公共接口 · API Reference

## <a id="deployment"></a>部署 · Deployment

## <a id="colors"></a>配色参考 · Color Reference

## <a id="logo"></a>项目标识 · Logo

## <a id="screens"></a>项目截图 · Screenshots

## <a id="opts"></a>性能优化 · Optimizations

## <a id="used"></a>使用者 · Used By

## <a id="profile-intro"></a>个人简介 · Github Profile - Introduction

## <a id="profile-about"></a>关于我 · Github Profile - About Me

## <a id="profile-links"></a>个人链接 · Github Profile - Links

## <a id="profile-skills"></a>个人技能 · Github Profile - Skills

## <a id="profile-other"></a>其他个人信息 · Github Profile - Other
