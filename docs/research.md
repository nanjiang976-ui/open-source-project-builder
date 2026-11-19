# 第一次把项目开源到 GitHub，怎样让别人用起来？

调研日期为 **2026 年 11 月 19 日**。这份报告写给已经有本地项目、准备第一次公开的作者。它帮助作者决定自己的首页先写什么、仓库里该放哪些材料，以及发布前如何判断别人能否用起来。

**如果这周只做一件事，挑一项陌生人能独立完成的小任务，亲自按 README 从头走一遍。** 例如，中文写作 Skill 的读者要交给它一段文字并收到改稿，浏览器扩展的读者要保存一张网页。两种项目的首页应把读者带往不同的入口。下面给出这项建议的样本依据，以及怎样用它整理自己的仓库。

## 研究怎样取样

GitHub 在采样时返回了该公开账号的 90 个收藏。从中有目的地选择 5 个不同用途的仓库，再补入 5 个能提供对照的仓库。特别保留了两个命令行工具和两个桌面软件，观察同一类项目如何因为文档规模、用户经验和核心卖点而采用不同首页。星数取当日读数的约数，固定提交链接保留当时分析的 README 与目录。后续重读时，收藏数和星数都可能变化。[公开收藏列表](https://github.com/nanjiang976-ui?tab=stars) · [GitHub 公开接口](https://api.github.com/users/nanjiang976-ui/starred?per_page=100)

阅读每个样本时，我们记录目标读者、首页的引导顺序、详细材料的位置，以及第一次操作应出现的结果。下文的“建议”是据样本作出的设计判断。研究查阅了项目方公开材料，未逐项安装这十个项目，也未组织新手可用性测试。星数用于寻找已有较广关注的样本，无法回答哪个 README 能带来更多星标。

## 来自公开收藏的五个案例

### 1. Humanizer-zh · 中文单 Skill · 约 2.3 万星

手里有一段中文或一个文档，想改善表达的人，进来先看到输入、默认产物，以及编辑时要保留的内容。随后是安装、验证安装、粘贴文本或指定文件，再看四组原文和改写。作者还注明示例使用教学输入，让读者知道效果展示的条件。

根目录的 `README.md` 面向人，`SKILL.md` 给智能体执行，`tests/` 留给验证，另有许可和更新记录。新手可以先交一段短文本，核对返回的改稿是否保留原有事实。对开源助手，最值得采用的是一组真实的“项目原状 → 用户请求 → 文件证据 → 如何补齐”。示例中的安装位置和调用方式与其目标客户端有关，Windows Codex 要单独验证。[固定版 README](https://github.com/op7418/Humanizer-zh/blob/f4518a8eab97b8bfebc66a89d34320a89bef6930/README.md) · [同版目录](https://github.com/op7418/Humanizer-zh/tree/f4518a8eab97b8bfebc66a89d34320a89bef6930)

### 2. mattpocock/skills · 工程 Skill 集合 · 约 32.8 万星

已经在借助 AI 开发、需要改善具体环节的人，先选自己使用的客户端，再为项目运行首次配置。正文用工程中反复碰到的问题解释技能为什么有用，最后按用途列出技能索引。选用技能前，读者先有机会认出自己的问题。

`skills/` 放实际技能，`docs/` 承载补充说明，`SCOPE.md` 和 `CONTRIBUTING.md` 告诉潜在贡献者项目接受什么。新手的第一项任务是完成自己环境的配置并找到对应技能。单一开源助手可借用“朋友照说明装不起来”“准备发新版，旧命令还适用吗”这样的触发表述。只有技能数量增多、需要在多种技能间选择时，才有必要增加分类索引。[固定版 README](https://github.com/mattpocock/skills/blob/5863806dd4e15c63174bee4e7515a4256792ecfa/README.md) · [同版目录](https://github.com/mattpocock/skills/tree/5863806dd4e15c63174bee4e7515a4256792ecfa)

### 3. yt-dlp · 命令行工具 · 约 20.9 万星

想通过终端获取媒体文件的人，先看到用途、目录和安装入口。发布文件表直接标明主流系统的推荐下载，随后列替代构建、更新方式、依赖，以及更详细的参数和配置示例。首个决定具体到“在我的系统上下载哪一个文件”。

`test/`、`Changelog.md` 和 `THIRD_PARTY_LICENSES.txt` 分别承载测试、变更和第三方许可。开源助手应借它的标注方式，把“下载、解压、复制哪个文件夹”写到足以辨认目标的程度。对功能较少的小工具，用一条最简单的命令配一个可见结果就能承担入门教学，完整参数表可按实际规模另设入口。[固定版 README](https://github.com/yt-dlp/yt-dlp/blob/2d596f4882a2d6e6414836bccd9fd3fb1e1534a2/README.md) · [同版目录](https://github.com/yt-dlp/yt-dlp/tree/2d596f4882a2d6e6414836bccd9fd3fb1e1534a2)

### 4. SingleFile · 浏览器扩展 · 约 2.3 万星

想保存网页的人先看到成果形式，再看演示、自己的浏览器商店和首次操作。上手步骤告诉读者打开网页、点击工具栏上的扩展按钮，保存一个 HTML 文件。读者知道完成时手里应该有什么。

`faq.md`、`known-issues.md`、`privacy.md` 和 `README-BUILD.md` 在根目录各自承担不同职责。用户保存网页时无需阅读如何构建扩展。开源助手可沿用这种分工，首页演示第一次检查，长篇研究单独保存。用“一条包含文件证据和下一步建议的发现”定义第一次成功。[固定版 README](https://github.com/gildas-lormeau/SingleFile/blob/5f36c0e0291290656202827884ea05fff8087e49/README.MD) · [同版目录](https://github.com/gildas-lormeau/SingleFile/tree/5f36c0e0291290656202827884ea05fff8087e49)

### 5. CC Switch · 桌面应用 · 约 15.6 万星

想在桌面管理 AI 开发工具配置的人，可以从页首的语言、下载及快速上手入口出发，再通过截图、各平台安装包和基本操作理解产品。页面还包含较长的赞助内容。对第一次来的读者，顶部直达入口缩短了找到安装步骤的路程。

多种语言的 README 分开维护，`docs/`、`SUPPORT.md`、`CONTRIBUTING.md` 和 `SECURITY.md` 服务想深入学习、求助、贡献和报告问题的人。对桌面软件，首个任务可以定为“选对安装包、打开应用、完成一次基本操作”。个人维护的首版可先把一种已验证语言和一个平台的教程写透，等其他平台完成实测再列为支持。[固定版 README](https://github.com/farion1231/cc-switch/blob/6a6ad60e7d6bf97d1cbb82c3149af373afbd97b7/README.md) · [同版目录](https://github.com/farion1231/cc-switch/tree/6a6ad60e7d6bf97d1cbb82c3149af373afbd97b7)

## 用于对照的五个案例

### 6. Requests · Python 开发库 · 约 5.5 万星

想在 Python 程序里发起 HTTP 请求的开发者，在读到安装前，就能看到请求代码以及状态码、响应数据等返回值。然后才进入安装、支持的 Python 版本、功能和克隆源码。几行具体调用足以让读者判断接口是否符合自己的使用方式。

`src/`、`docs/`、`tests/` 分别存放实现、长文档和测试。第一次的目标是发出一个请求并认出返回结果。借到 Skill 首页上，就是把一句可以复制的中文提问和一小段实际回答放在安装教程前。读者可以据此判断输出是否有用，首次安装成功与否仍要亲自验证。[固定版 README](https://github.com/psf/requests/blob/3c7baaa05ab4aa49cc819ce3a819d260de19c157/README.md) · [同版目录](https://github.com/psf/requests/tree/3c7baaa05ab4aa49cc819ce3a819d260de19c157)

### 7. ripgrep · 命令行搜索工具 · 约 7 万星

想在代码目录中查找文本的人，先看到默认搜索行为、支持平台与文档入口，再看到示例、性能比较、适用情形与局限，之后可查安装、构建和测试。性能比较附有语料、命令和运行条件，读者能够理解数字是怎样得出的。

`GUIDE.md` 和 `FAQ.md` 让用户深入查用法，维护者另有 `RELEASE-CHECKLIST.md`。新手可以挑一个自己知道存在的字符串执行搜索，对照终端匹配结果。开源助手可学它说明“默认检查哪些内容、凭什么得出这一结论”。当项目卖点不依赖性能时，给一条可复核的输入与输出，比添加基准测试章节更有用。[固定版 README](https://github.com/BurntSushi/ripgrep/blob/fdf7d95485ec69c599418b7e7154baa4518fed2c/README.md) · [同版目录](https://github.com/BurntSushi/ripgrep/tree/fdf7d95485ec69c599418b7e7154baa4518fed2c)

### 8. Immich · 自部署照片应用 · 约 12 万星

想自己托管照片库的人，需要判断功能是否合用，也要知道个人数据如何保护。首页展示界面、语言和备份提醒，提供文档与安装入口，然后给可访问的演示和手机端／网页端功能对照。首次体验和正式部署各有路径。

`mobile/`、`web/`、`server/` 对应客户端和服务端，`docker/`、`deployment/` 和 `docs/` 支持部署与深入阅读。普通读者可以先看演示，部署者则需要跑通自己的安装。开源助手可以先提供一份已完成的检查结果，让人低成本判断是否需要安装。只有应用真的提供演示实例时，首页才应承诺在线试用。[固定版 README](https://github.com/immich-app/immich/blob/ac9362f1010b590825d6090804c7d784d54d610c/README.md) · [同版目录](https://github.com/immich-app/immich/tree/ac9362f1010b590825d6090804c7d784d54d610c)

### 9. OBS Studio · 成熟桌面软件 · 约 8 万星

想录屏的用户、要编译源码的人、插件开发者、翻译贡献者都可能进入同一仓库。README 简介后，快捷入口分别通往官网、帮助、论坛、编译、开发 API 和报错，后面才谈贡献。普通用户的第一步可以是进入官网获取应用或打开使用帮助。

`frontend/`、`libobs/`、`plugins/` 分开承载桌面前端、核心库和插件。`CONTRIBUTING.md`、`CODESTYLE.md`、`SECURITY.md` 为需要参与维护的人提供入口。成熟项目能够用一张简短导航页服务多种读者，靠的是每个链接后面已有完整内容。刚发布的个人项目应先在仓库本身写完整一条上手路径。[固定版 README](https://github.com/obsproject/obs-studio/blob/717cfa8b7e633853cd21ad2cc656185b3b4255bb/README.rst) · [同版目录](https://github.com/obsproject/obs-studio/tree/717cfa8b7e633853cd21ad2cc656185b3b4255bb)

### 10. First Contributions · 新手实践教程 · 约 5.7 万星

想第一次向开源项目提交改动的人，可以选择图形界面教程，或按主线准备 Git、派生仓库、克隆、建分支、改文件、提交、推送并发起拉取请求。旧版 Git 的替代命令和推送认证问题就放在容易卡住的步骤旁。

`Contributors.md` 是读者真正动手的文件，`docs/` 提供补充材料。首次成功有一个可检查的外部结果，即读者发出的拉取请求。可以学这种“一次只做完一件事”的教程设计，把开源助手最常见的安装层级错误和识别方法紧贴安装步骤。普通项目的首次任务应以真实用户目标为准，发起拉取请求只适合本身旨在教人贡献的教程。[固定版 README](https://github.com/firstcontributions/first-contributions/blob/b2f6bca4833e8c66a918925ddb2da60200ebd294/README.md) · [同版目录](https://github.com/firstcontributions/first-contributions/tree/b2f6bca4833e8c66a918925ddb2da60200ebd294)

## 直接协助作者开源的项目和资料

| 作者遇到的问题 | 从哪里开始、怎样使用 | 能得到的结果 |
|---|---|---|
| 从自用转为公开，首先想清楚什么？ | 阅读中文版《开始一个开源项目》，写下希望谁来使用、如何参与，再逐项对照公开前检查。[GitHub 开源指南](https://opensource.guide/zh-hans/starting-a-project/) | 一份解释为什么开源、准备开放哪些材料、接下来要补什么的简短清单。 |
| 仓库里不同文件各做什么？ | 看瑞典数字政府机构 DIGG 的模板，区分模板项目自己的文档与 `templates/` 内供其他项目采用的材料，挑选适用项并替换占位内容。[模板仓库](https://github.com/diggsweden/open-source-project-template) · [检查清单](https://github.com/diggsweden/open-source-project-template/blob/main/docs/Open_Source_Checklist.md) | 可用的目录参考和发布检查表，适合决定 README、许可、贡献和协作材料怎样分工。 |
| 我不熟 Markdown，怎样起草首页？ | 用 Best-README-Template 的空白版选择章节，或在 readme.so 选择、排序、预览、下载。安装命令、配置及截图均改成自己跑过的内容。[空白模板](https://github.com/othneildrew/Best-README-Template/blob/fc444eb7b04b2e4863f6080b1507a219e95103fa/BLANK_README.md) · [readme.so](https://readme.so/editor) | 一份可以继续填写的首页。发布前还需要实际走完示例。 |
| 多个开发库想采用一致写法 | Standard Readme 有面向开源库的章节规范、生成器和样例。可以对照安装、调用、维护和贡献章节。[Standard Readme](https://github.com/RichardLitt/standard-readme) | 库的使用者知道去哪里找最小代码示例和 API 文档。 |
| 已经公开，怎样知道 GitHub 识别了哪些社区资料？ | 打开仓库的社区档案，核对平台识别的 README、许可、贡献等文件。把发现的缺项与项目实际参与方式对照。[GitHub Community Profile](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/about-community-profiles-for-public-repositories) | 一份文件层面的检查结果，另外安排首次使用演练来验证教程。 |
| 可以把代码放上网，别人具体能做什么？ | 先理清自己的代码和第三方材料分别由谁授权，再选择符合意图的许可证。GitHub 的公开仓库提供查看和平台允许的派生能力。跨项目使用、修改和再分发应查看授予的许可。[Choose a License](https://choosealicense.com/no-permission/) | 作者确认的授权条件，以及需要保留的第三方许可或署名。 |

## 把研究用于下一个项目

### 根据用户第一次要做的事安排首页

| 项目类型 | 首页最该让读者找到什么 | 作者验收时观察什么 |
|---|---|---|
| Skill | 什么情形要叫它、在哪个客户端输入哪句话、预期拿到什么 | 新环境能识别 Skill，一次真实请求得到符合职责的可辨认结果。 |
| 命令行工具 | 选哪个发行文件、在哪输入命令、要准备哪个文件 | 复制最短命令能运行，输出与说明匹配。 |
| 开发库 | 版本与依赖、最小调用、返回值 | 新建环境安装后，代码能执行，返回结果与样例相符。 |
| 桌面软件或扩展 | 下载入口、合适的安装包、首次点击、保存位置 | 读者能走正常安装入口，观察到首次点击的结果。 |
| 自部署应用 | 能否先体验、运行环境、配置示例、启动与访问入口 | 从干净配置启动后可访问服务，必要的数据存储和备份要求已交代。 |
| 教程或模板 | 要改哪个真实对象、改完会发生什么 | 读者能完成一次练习或得到能使用的项目副本。 |

### 一个作者可以执行的发布顺序

1. **圈定公开内容。** 列出现成实现、样例、图片和配置。检查会随发布一起公开的文件与已有提交历史，确认没有不宜公开的资料。让作者确认授权，再在许可说明中保留需要的署名或第三方条款。[GitHub 开源指南](https://opensource.guide/zh-hans/starting-a-project/)
2. **用一条用户任务搭出 README。** 先写“谁手里有什么，完成后能得到什么”，再补安装和操作位置。比如一个返回处理结果的小工具，给最小输入文件、命令及预期产物。截图适合展示界面变化，命令行则更适合可复制的文本。
3. **跟着文字试一次，把证据放回合适的位置。** 从新的副本或隔离环境测试，记录系统、版本、实际输入与结果。把导致中断的问题补在出错的步骤旁。已有文档中写着“测试通过”、仓库里存在测试文件、此次真正运行并通过，分别记录。
4. **给读者留一个可用的反馈入口。** 写明遇到问题时要附版本、操作步骤和错误信息。仓库已开放 Issues 时可以直接链接。通过本地文件分发时，可告诉读者要把哪些信息反馈给提供文件的人。开始持续接收外部贡献后，再按维护需求补 `CONTRIBUTING.md` 和问题模板。[GitHub 社区档案](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/about-community-profiles-for-public-repositories)
5. **决定什么时候公开。** 作者核对许可、将要公开的材料以及真实可达的下载入口，再决定建仓或发布版本。此后每次改安装方式、依赖或用户入口，都复跑 README 中相应的示例。

本项目的首页带首次开源的作者从使用场景走到第一次调用。安装进 Agent 的 `SKILL.md` 说明怎样按项目类型检查，本文保留这些设计的依据。Agent Skills 规范要求技能描述交代能力和使用时机，因此首页给人的承诺应与实际技能指令一致。[本项目 README](../README.md) · [Agent Skills 规范](https://agentskills.io/specification)
