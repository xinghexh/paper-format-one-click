# DeepSeek Harness（DSH）安装与兼容说明

## 当前支持方式

本项目是标准的 Skill 目录包，入口为仓库根目录 `SKILL.md`，标识名 `paper-format-one-click` 符合 DSH 的 kebab-case 命名要求。DSH 本地 Skill Provider 能发现 `<name>/SKILL.md` 形式的目录包，因此可以将此仓库直接放入用户或项目的 Skill 目录。

安装到当前用户：

```powershell
git clone https://github.com/xinghexh/paper-format-one-click.git "$env:USERPROFILE\.dsh\skills\paper-format-one-click"
```

项目内安装：将仓库放入项目根目录下 `.dsh/skills/paper-format-one-click/`。DSH 文档还列出 `.agents/skills` 等发现目录；若放在自定义目录，需要确保当前 profile 已配置该目录。

安装后刷新/重启 DSH 会话，并在 Skill 列表中确认 `paper-format-one-click` 可见。标准流程需要 DSH profile 中启用本地 Skill 文件系统 Provider（`@deepseek-ai/dsh-skill-filesystem`）和模型侧 Skill Consumer（`@deepseek-ai/dsh-tool-skill`）；不同版本或 profile 的启用方式可能有差异，应遵循当前安装版本的官方说明。

## Skill 与 DSH 插件包的区别

- **Skill** 是可发现并由模型加载的工作指令和配套资料。本项目现有内容属于这一类，可通过 DSH 本地 Skill 目录使用。
- **DSH 插件包**是额外的 Cordis 代码插件，需定义插件元数据/组合配置并实现代码入口。当前项目没有运行时代码，因此不应把它称为已经打包好的 DSH 插件，也不需要为加载普通 Skill 增加自定义插件代码。

## 能力边界

Skill 负责指导期刊官网规范检索、样式学习、中文论文标题/表格格式、图表题注和交叉引用、参考文献整理及交付核查。它本身不提供 Word 自动化、文件系统访问或浏览器能力。DSH 执行环境必须另外提供相应工具；若没有 DOCX 编辑/渲染能力，只能给出操作步骤和核查建议，不能声称已直接完成 Word 排版。

## 官方资料

- [DSH Skills 子系统文档](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/skills.md)：本地目录发现、命名规则、Skill Provider 和 Consumer。
- [DSH 本地 Skill 文件系统 Provider](https://github.com/deepseek-ai/deepseek-harness/tree/master/packages/skill/skill-filesystem)：目录 Skill 的发现方式和配置。
- [DSH 插件开发文档](https://deepseek-harness.github.io/deepseek-harness/en/develop/basic/)：Cordis 插件的开发方式；独立插件包需按此体系构建。

> 兼容性说明依据官方文档所述的文件结构与发现机制整理。没有在本项目环境中安装 DSH，因此不代表已完成特定 DSH 版本的运行时验收；版本或 profile 差异应按对应版本文档复核。
