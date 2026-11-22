# 项目开源助手维护规则

## 项目入口

- 使用说明、安装方式和贡献入口见 [README](README.md)。外部贡献按 [贡献说明](README.md#contributing) 提交。
- 可安装目录位于 [skills/open-source-project-builder/](skills/open-source-project-builder/) 下。[SKILL.md](skills/open-source-project-builder/SKILL.md) 定义助手行为，[references/](skills/open-source-project-builder/references/) 保存按需读取的详细流程。

## 提交与合入

- 每次提交集中处理一件事，维护提交用简短的英文动词短语写清改动，例如 `Document project maintenance rules`。
- 维护者明确授权的小改动可以快进推送到 `main`。外部贡献、影响用户使用流程的改动，以及改变文件写入或发布行为的改动，都通过 PR 合入。

## 验证

- 文档变更核对文件路径、链接和锚点，检查复制使用的示例及受影响的章节。
- Skill 行为变更用临时项目实际调用，记录触发请求、预期结果、使用的 Agent 和实测结果。
- 更新源码 ZIP 时，将包内文件与对应的发布提交逐文件比对。

## 版本与 Release

- 有用户可感知的变化且验证通过时，由维护者决定是否手动发版。版本标签采用 `v主.次.补丁`，首个具体版本号在首次 Release 时确定。
- 稳定版修复问题且兼容既有用法时升补丁号，新增兼容功能时升次版本号，破坏已承诺的调用或安装方式时升主版本号。
- 发布前核对已验证的提交、标签所指向的提交、发行说明和下载物。推送标签、保存远端草稿以及公开 Release 均按维护者授权执行。
- 发布后，从该版本的 Release 页面下载读者实际会用的文件，在干净目录按 README 走通首次使用，并记录结果。
